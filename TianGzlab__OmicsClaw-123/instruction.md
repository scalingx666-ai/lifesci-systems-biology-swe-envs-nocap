# Issue

**Title:** refactor(bot): finish skill_orchestration + extract tool_executors (PR-A)

## Description

## Summary

PR-A of the post-#122 follow-up. Closes the remaining mechanical-extraction issues (#119 reduced scope + #120) on the path toward a thin `bot/core.py` facade. **`bot/core.py` 3811 → 1441 LOC (−72.1% cumulative from the 5160-LOC baseline on main pre-PR #122).**

PR-B (a separate branch / PR) will land #121 — `bot/agent_loop.py` extraction with new deep-module unit tests against a fake LLM client + final facade collapse.

Refs PRD #113, ADR 0001 (local), milestone "bot/core decomposition".

## What ships

| Commit | Issue | Module | LOC moved | New tests |
|---|---|---|---|---|
| `67b46c5` | #119 (remainder) | `bot/skill_orchestration.py` (extended 116 → 771) | ~620 | identity test (1) |
| `70c88d2` | #120 | `bot/tool_executors.py` (new, 1900 LOC) | ~1750 | identity + dispatch sanity (2) |

Coordination follow-up from PR #122 review Important #2 also done: `omicsclaw/runtime/preflight/sc_batch.py` now imports `_run_omics_skill_step` from `bot.skill_orchestration` and `execute_omicsclaw` from `bot.tool_executors` (their canonical homes), not via the `bot.core` re-export.

### Backward-compat enforcement

Three identity-comparison test files (`tests/bot/test_billing.py`, `tests/bot/test_skill_orchestration.py`, `tests/bot/test_tool_executors.py`) collectively pin **52 symbols** to be the *same Python object* on both `bot.core` and the canonical home — a refactor that breaks any of them produces an immediate AssertionError.

External regression suite untouched: `tests/test_bot_*.py`, `tests/test_oauth_regressions.py`, `tests/test_app_server.py`, `tests/test_notebook_files.py`, `tests/test_routing_regression.py`, `tests/test_auto_routing_disambiguation.py`, `tests/test_skill_listing.py` all pass without modification.

## Cross-module access patterns

Each carved-out module follows the same convention:

* **Stable bot.core symbols** (path constants, `registry`, `audit`, `logger`, in-place-mutated dicts like `received_files`) imported at module top.
* **Runtime-reassigned globals** (`memory_store`, `llm`, `OMICSCLAW_MODEL`, `LLM_PROVIDER_NAME`, `session_manager`) accessed via `_core.<name>` at call time. Source rewritten via sed to use the `_core.X` form. This lets `bot.session.init()` set them after modules finish loading without snapshots going stale.
* **Sibling helpers** (`bot.skill_orchestration`, `omicsclaw.runtime.preflight.sc_batch`) imported from canonical homes, not via `bot.core` re-export.

## Verification

- [x] `pytest tests/test_bot_*.py tests/test_oauth_regressions.py tests/test_skill_listing.py tests/test_routing_regression.py tests/test_auto_routing_disambiguation.py tests/test_app_server.py tests/test_notebook_files.py tests/test_bot_core_timeout.py tests/bot/ tests/runtime/preflight/`: **228 passed, 1 skipped, 4 xfailed** — no regressions.
- [x] `pytest tests/eval/ tests/test_knowhow.py`: **121 passed, 17 deselected**. Behavioural-parity baseline 14/15 against `deepseek-v4-pro` unaffected.
- [x] `python -c "import bot.core; assert bot.core.execute_omicsclaw.__module__ == 'bot.tool_executors'; assert bot.core._run_omics_skill_step.__module__ == 'bot.skill_orchestration'"` — canonical homes verified.

## What's left for PR-B

* `bot/agent_loop.py` — `llm_tool_loop` + AsyncOpenAI client lifecycle + `_ensure_system_prompt` + `get_tools` / `_build_bot_tool_context` / `_build_llm_timeout`.
* `tests/bot/test_agent_loop.py` — deep-module unit tests against a fake LLM client (single-round / multi-round tool dispatch / inspection-only round / streaming / error paths).
* Final `bot/core.py` collapse to thin facade (~150 LOC).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e4dc05fc69d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.