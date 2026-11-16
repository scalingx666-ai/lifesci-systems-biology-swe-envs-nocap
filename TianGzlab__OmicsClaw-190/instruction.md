# Issue

**Title:** refactor(executor): async-native SkillRunnerExecutor, drop asyncio.to_thread (OMI-12 audit P1 #4)

## Description

## Summary
OMI-12 audit 🟡 P1 #4 — last item in the post-P2.9 backlog. `SkillRunnerExecutor.run` used to do `await asyncio.to_thread(run_skill)`, which parks one `ThreadPoolExecutor` worker per active skill. Under multi-user app-server load with long-running skills (`velocity`, `pseudotime`, …) the default 32-worker pool can fill up and stall unrelated async work. This PR rewires the executor onto the same `asyncio.create_subprocess_exec` strategy that `SubprocessExecutor` already uses.

## What changes

| File | Change |
|---|---|
| `omicsclaw/core/runtime/async_subprocess_driver.py` | **New.** `adrive_subprocess` — async sibling of `drive_subprocess`. Same status-field + `-9 → 0` fallback semantics; `start_new_session=True` for process-group cancel; `asyncio.CancelledError` propagates after SIGTERM → grace → SIGKILL. |
| `omicsclaw/core/skill_runner.py` | Extracted `_prepare_skill_run` + `_finalize_skill_run` helpers so the sync `run_skill` and the new async `arun_skill` share the same skill resolution, argv build, env setup, and output-finalize logic. Added `arun_skill` as the async entry point. |
| `omicsclaw/execution/executors/default.py` | `SkillRunnerExecutor.run` now `await`s `arun_skill` directly. The blocking `_run` closure, the `asyncio.to_thread` wrap, and the `threading.Event` cancel-bridge are all gone. |

## What does NOT change

- The sync `run_skill` stays — CLI, bot, and pipeline-runner callers continue to use it. The bot's per-line `stdout_callback` / `stderr_callback` streaming flows through the sync subprocess driver as before.
- `_err`, `resolve_skill_alias`, pipeline dispatch (`<name>-pipeline`), and `SkillRunResult` return shape are preserved byte-for-byte.
- `JobOutcome` shape returned by `SkillRunnerExecutor` is unchanged — same `exit_code` / `error` / `stdout_text` fields.

## New tests

- **`tests/test_async_subprocess_driver.py` (4 tests)** — corner cases for `adrive_subprocess`:
  - stdout and stderr captured separately
  - legacy `-9 + result.json exists → 0` heuristic still fires
  - `status: ok` overrides a non-zero exit (P1 #2 contract preserved)
  - `asyncio.CancelledError` kills the process group even when the child ignores SIGTERM (the grace-period SIGKILL escalation closes the run within ~5s instead of leaking)
- **`tests/test_execution_default_executor.py`** — three existing tests rewritten to monkeypatch `arun_skill` instead of `run_skill` (no more `cancel_event` assertion since the async path doesn't need it). One **new** regression test counts `asyncio.to_thread` calls during `SkillRunnerExecutor.run` and fails if any sneak back in.

## Test plan
- [x] `pytest tests/test_async_subprocess_driver.py tests/test_execution_default_executor.py tests/test_execution_executors.py` — 20 passed, 1 skipped; 1 pre-existing env failure unrelated (`fastapi` missing).
- [x] Wider sweep across `tests/test_async_subprocess_driver.py tests/test_execution_*.py tests/test_skill_runner_contract.py tests/test_output_ux.py tests/test_result_status_contract.py tests/test_runtime_*.py tests/test_registry.py tests/test_capability_resolver*.py tests/test_routing_regression.py tests/test_bot_n_epochs_routing.py` — 132 passed, 2 skipped, 5 xfailed; 2 pre-existing env failures unrelated.
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_bot_runner_contract.py tests/test_interactive_omicsclaw_actions.py tests/test_autoagent_cli.py` — 107 passed; same 4 pre-existing failures as `main`.
- [x] `python omicsclaw.py list` — 89 skills × 8 domains.

## Backlog

This was the last item on the user's OMI-12 audit list (`P1 #4 SkillRunnerExecutor → async-native`). After this PR the original OMI-12 evaluation's P0/P1/P2 + audit-surfaced P0/P1 items are all landed:

- ✅ P0.1 stale `SKILLS` cache + P0.2 `import json` + P0.3 private-field poking (PR #181)
- ✅ P1.4 carve `run_skill` + P1.5 delete `LocalExecutor` (PR #182)
- ✅ P1.6 `run_skill` native `SkillRunResult` (PR #184)
- ✅ P2.7 YAML pipelines (PR #185)
- ✅ P2.8 documented weights + P2.9 golden routing snapshot (PR #186)
- ✅ Audit P0 WGCNA tie-break + bot dead branches (PR #187)
- ✅ Audit P1 #1 single iter + P1 #3 `should_search_web` default (PR #188)
- ✅ Audit P1 #2 `result.json` status contract (PR #189)
- ✅ Audit P1 #4 async-native executor (this PR)

P3 (structured event logs, per-skill timeout, embedding routing) was deferred at the user's request from the start.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c6ac3872681`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.