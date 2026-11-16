# Issue

**Title:** fix(bot): clean up bot-core carve-out fallout (NameErrors + stale-reference + dead code)

## Description

## Summary

Six fixes landing as three logical commits, all under one root cause: the
``bot/core.py → bot/tool_executors.py + bot/path_validation.py + …``
carve-out per ADR 0001 (#120 / #192 / #193) left several module-level
names un-imported in the carved-out files, and one helper (``_ensure_trusted_dirs``)
rebound a shared global instead of mutating in place. Each one was a
latent runtime bug — only the first one had been observed in production
so far (2026-05-13 user incident).

## What was wrong

| # | Bug | Where | Symptom |
|---|---|---|---|
| 1 | ``_ensure_trusted_dirs`` / ``TRUSTED_DATA_DIRS`` / ``validate_input_path`` / ``discover_file`` / ``resolve_dest`` / ``sanitize_filename`` / ``validate_path`` un-imported | ``bot/tool_executors.py`` | ``NameError: name '_ensure_trusted_dirs' is not defined`` on ``omicsclaw({"mode":"file"})`` |
| 2 | ``DEEP_LEARNING_METHODS`` / ``OMICSCLAW_PY`` / ``_path_names`` / ``_infer_skill_for_method`` / ``_run_skill_via_shared_runner`` / ``_resolve_requested_batch_key`` un-imported | ``bot/tool_executors.py`` | Latent NameError on the matching execute_* code paths |
| 3 | ``_ensure_trusted_dirs`` rebound the global instead of mutating in place | ``bot/path_validation.py`` | ``execute_list_directory`` rejects legit DATA_DIR with ``Access denied … is not in trusted directories ()`` — list shown empty even though path_validation's own copy is populated |
| 4 | ``bot.core.TOOLS`` ``__getattr__`` branch calls ``get_tools()`` without importing it | ``bot/core.py`` | ``NameError: name 'get_tools' is not defined`` on every ``bot.core.TOOLS`` access |
| 5 | ``Optional`` used five times but never imported (PEP 563 masks it) | ``omicsclaw/knowledge/registry.py`` | Latent — fires on ``typing.get_type_hints`` (Pydantic / FastAPI / future-import removal) |
| 6 | Dead branch ``target_path = DATA_DIR / target_path`` after a ``return`` | ``bot/tool_executors.py`` (``execute_make_directory``) | Forgotten fallback; current hard-deny behavior is already safe |

## Methodology

- **TDD red-green-refactor** for each fix: write a failing regression
  test that pins the runtime contract (not just import-time presence),
  apply the minimal fix, re-run the test.
- **pyflakes** sweep across ``bot/`` and ``omicsclaw/`` to find the rest
  of the same class of bug (undefined names).
- **Dynamic ``execute_*`` harness** (``/tmp/oc_executor_probe.py`` —
  not committed) ran 36 minimal-arg scenarios across all 24 executors;
  no remaining ``NameError`` / ``AttributeError`` on our own symbols.
- **AST sweep** for ``statement-after-terminator`` flagged the one dead
  branch.
- **``global X; X = build()`` rebind-pattern audit** across 11 sites in
  the repo — all others use a getter or aren't imported by reference,
  so #3 is the only stale-reference bug.

## Test plan

- [x] ``pytest tests/bot/test_tool_executors.py`` (4 new tests pass, plus
      existing identity / dispatch tests)
- [x] ``pytest tests/test_bot_core_import_behavior.py`` (1 new test pass,
      plus existing 2 import-behavior tests)
- [x] ``pytest tests/test_knowledge_registry.py`` (1 new test pass, plus
      existing 2 frontmatter tests)
- [x] Wider bot suite: net **+7 passing, 0 regressed** (baseline failures
      are a pre-existing pydantic-v2 env issue and a test-isolation
      issue in ``test_context_layer_predicate.py`` — both unrelated)
- [x] CLI smoke: ``python omicsclaw.py list`` and ``omicsclaw doctor``
      run clean
- [x] Dynamic harness: all 36 ``execute_*`` probe scenarios return
      strings; ``execute_list_directory(DATA_DIR)`` now returns the
      actual file listing instead of ``Access denied … ()``

## Commits

1. **fix(bot): restore path_validation + carved-out sibling imports in tool_executors**
   — addresses #1 and #2 above
2. **fix(bot): in-place TRUSTED_DATA_DIRS mutation + lazy bot.core.TOOLS resolution**
   — addresses #3 and #4 above
3. **chore(bot+registry): import Optional in knowledge.registry + drop dead branch in make_directory**
   — addresses #5 and #6 above

## Known related issue (out of scope)

``omicsclaw/runtime/context_layers/__init__.py:573`` uses
``Callable[["events.LifecycleEvent"], None]`` without importing the
``events`` submodule. Tried to fix; the eager import triggers a real
circular load (``omicsclaw.runtime.__init__`` re-enters
``context_layers`` mid-load), breaking
``test_predicate_evaluation_emits_hit_and_miss_events``. The existing
``# local import to avoid cycles`` comment was load-bearing. Kept latent
— no current call site touches ``get_type_hints`` on the signature.
Worth tracking separately.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Fixed path validation and trusted directory checks for file operations and tool execution.
  * Improved reliability of tool availability and error messaging when executing certain operations without required inputs.
  * Enhanced directory handling to ensure validation checks remain effective across modules.

<!-- review_stack_entry_start -->

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/194)

<!-- review_stack_entry_end -->

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ddd5a4441c58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.