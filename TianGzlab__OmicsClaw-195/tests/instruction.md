# Issue

**Title:** Fix: stop LLM tool-call loop on malformed omicsclaw args

## Description

## Summary

Fixes the failure mode where, in CLI use, the agent receives a prompt like *\"对 pbmc3k_raw.h5ad 执行预处理\"* and ends up looping through tool calls until it hits ``MAX_TOOL_ITERATIONS=20`` and returns *\"(max tool iterations reached)\"* with no analysis run.

**Root cause (verified by audit log replay + direct repro):** the LLM hallucinates a nested arg shape — ``{\"params\": {\"input\": \"/x.h5ad\"}}`` — instead of the schema-declared top-level ``file_path``. ``execute_omicsclaw`` silently drops the unknown ``params`` key, then falls through to the generic *\"No input file available. You can either: 1. Upload a file via messaging...\"* fallback. The LLM reads that as a missing-file problem rather than an arg-shape problem and pivots to ``glob_files`` / ``file_read`` exploration, burning the remaining iteration budget. Eight consecutive omicsclaw calls in ``bot/logs/audit.jsonl`` all used the malformed shape; the model never self-corrected.

Two-layer fix:

1. **Server-side validator** (``bot/tool_executors.py``) — new ``_validate_omicsclaw_args`` runs at the top of ``execute_omicsclaw`` before any I/O. Allowed-key set is derived from the ``omicsclaw`` ``ToolSpec.parameters[\"properties\"]`` at module load (single source of truth — schema changes auto-propagate). Returns an LLM-readable error naming the rejected keys and proposing the closest schema key via ``difflib.get_close_matches``. The documented ``params`` nesting case gets an explicit top-level ``file_path`` hint. Runtime-internal flags (``confirmed_preflight``) are whitelisted so the preflight auto-prep self-recursion doesn't trip its own guard.

2. **Client-side priming** (``omicsclaw/runtime/bot_tools.py``) — the ``omicsclaw`` tool description now carries a concrete ``mode='path', file_path='/abs/path.h5ad'`` example plus an explicit anti-``params`` callout and a ``mode='file' is only for chat uploads`` clarification. Defense in depth: even without the server validator, the LLM has an in-context anchor against the training-prior nesting pattern.

**After fix**, the repro that previously produced *\"No input file available...\"* now returns:

> Unknown parameter(s) in omicsclaw call: ['params'].
> Note: the omicsclaw tool does not accept nested 'params'. Pass path as ``file_path='/abs/path.h5ad'`` at the top level.
> Accepted keys: ['auto_prepare', 'batch_key', 'confirm_workflow_skip', 'data_type', 'extra_args', 'file_path', 'method', 'mode', 'n_epochs', 'query', 'return_media', 'skill'].

— a one-turn recoverable error that names the rejected key, points at the correct top-level key, and lists the schema for clarity.

Diff: **3 files, +212/−1 LOC** across 4 commits (TDD slice per commit + a fourth review-polish commit that tightens the integration test's path portability and strengthens the description-pin).

## Test plan

- [x] ``python -m pytest tests/bot/test_execute_omicsclaw_validation.py -v`` — 7/7 new tests green (5 unit + 1 integration + 1 description-pin).
- [x] Full Phase 1/2 regression suite (``tests/test_no_reverse_imports.py``, ``tests/engine/``, ``tests/bot/``, ``tests/test_bot_agent_loop_imports.py``, ``tests/test_compact_slash_command.py``, ``tests/test_channels.py``): **150 passed, 4 errors**. The 4 errors are the pre-existing pydantic v1/v2 collection failures in ``tests/bot/test_skill_orchestration.py`` ×2 and ``tests/bot/test_tool_executors.py`` ×2 — confirmed unchanged against baseline.
- [x] Boundary guardrail: ``GRANDFATHERED_LAZY_IMPORTS`` still 12 — no new reverse imports.
- [x] Diagnose-style repro: ``execute_omicsclaw`` with the audit-log-shape malformed args now returns the actionable validator error mentioning ``file_path`` and no longer matches the legacy *\"Upload a file via messaging\"* fallback. Verified one final time on the rebased branch HEAD.

## Reviewer guidance

- **Architecture:** the allowed-key set is derived from the tool spec at module load. Adding a new property to ``omicsclaw`` ``ToolSpec.parameters[\"properties\"]`` in ``omicsclaw/runtime/bot_tools.py`` auto-extends what the validator accepts — no parallel hardcoded list to drift.
- **Direction:** all imports remain ``bot/ → omicsclaw/runtime/`` (forward). No new reverse boundary violations.
- **Where to focus:** ``_validate_omicsclaw_args`` in ``bot/tool_executors.py`` (the new module-level constants + the 30-LOC helper) and the additions to the ``omicsclaw`` ``ToolSpec.description`` block in ``omicsclaw/runtime/bot_tools.py``.

## Out of scope (separate slices)

- Enabling OpenAI ``strict`` tool-schema mode — DeepSeek doesn't honor it tightly anyway, and the server-side validator covers the same gap with a more actionable error.
- Deprecating ``mode='file'`` entirely for CLI use — the description clarification covers the immediate footgun.
- The 4 pre-existing pydantic v1/v2 ``ImportError``s in ``tests/bot/test_skill_orchestration.py`` and ``tests/bot/test_tool_executors.py`` — environment-only, unrelated to this fix; new tests live in a separate file to avoid the collection failure.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ddd5a4441c58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.