# Issue

**Title:** refactor(skill-runner): carve run_skill into runtime subpackage + drop LocalExecutor (OMI-12 P1.4+P1.5)

## Description

## Summary
Pure refactor PR — addresses OMI-12 P1.4 (split the 634-line `run_skill` god-function) and P1.5 (delete the dead `LocalExecutor` stub). Zero contract change; all existing tests pass.

### P1.4 — carve `omicsclaw/core/skill_runner.py` into 4 focused modules

`omicsclaw/core/skill_runner.py` shrinks from **632 → 299 LOC**; `run_skill` itself from ~250 → ~110 lines. Heavy lifting moves to `omicsclaw/core/runtime/`:

| Module | Responsibility |
|---|---|
| `runtime/argv_builder.py` | Argv assembly + LLM-supplied flag filter; the `--epochs` ↔ `--n-epochs` alias rewrite; `--input` / `--output` / `--demo` always-blocked list. |
| `runtime/subprocess_driver.py` | `Popen` + orphan reaper + cancel watcher + per-line stdout/stderr streaming; returns a `subprocess.CompletedProcess`. The `-9 → 0` heuristic stays here, with the `was_cancelled` guard preserved. |
| `runtime/output_finalize.py` | Output-directory rename, `README.md`, reproducibility notebook generation; pipeline README. |
| `runtime/pipeline_runner.py` | `SPATIAL_PIPELINE` constant and the chain driver. Late-imports `run_skill` to keep the DAG one-way. |

`skill_runner.py` remains the public entry point. Backward-compat aliases (`_extract_flag_value`, `_build_user_run_command`, `_finalize_output_directory`, `_write_pipeline_readme`, `_deduplicate_path`, `DEFAULT_OUTPUT_ROOT`, `SPATIAL_PIPELINE`) are re-exported so existing test monkey-patches keep working.

### P1.5 — drop `LocalExecutor`

`LocalExecutor` was a legacy `executor_not_implemented` stub. The only real usage was as a test stub for `tests/test_remote_routes_contract.py`; `jobs.py` imported `EXECUTOR_NOT_IMPLEMENTED_LINE` from it at runtime. Cleanup:

- Delete `omicsclaw/execution/executors/local.py`.
- Drop `LocalExecutor` from `executors/__init__.py`.
- Inline `EXECUTOR_NOT_IMPLEMENTED_LINE` into `omicsclaw/remote/routers/jobs.py` (its only runtime consumer).
- Replace `LocalExecutor()` in `tests/test_remote_routes_contract.py` with an inline `_NotImplementedStub` class.
- Rewrite `tests/test_execution_executors.py` around the `Executor` Protocol shape rather than the now-removed concrete stub.

### New tests
`tests/test_runtime_argv_builder.py` adds 18 focused unit tests for the carve-out helpers:
- `extract_flag_value` edge cases: equals form, trailing flag, empty input
- `filter_forwarded_args`: allow-listed only; `--input` / `--output` / `--demo` always blocked even if mistakenly allow-listed; `--epochs` ↔ `--n-epochs` rewrite both directions; inline equals form preserved; negative numeric values treated as values not flags
- `build_skill_argv`: returns `None` when no input/demo source provided; demo-args expansion; multi-input vs single-input vs demo shapes
- `build_user_run_command`: demo form, input + forwarded-args form

## Test plan
- [x] `python omicsclaw.py list` — 89 skills × 8 domains ✓
- [x] `pytest tests/test_runtime_argv_builder.py` — 18/18 new tests pass
- [x] `pytest tests/test_skill_runner_contract.py tests/test_output_ux.py tests/test_execution_default_executor.py tests/test_execution_executors.py tests/test_registry*.py` — 50 passed, 1 skipped (needs fastapi), 2 pre-existing env failures (`scanpy` / `fastapi`) unchanged from main
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_bot_runner_contract.py` — 99 passed, 2 errors + 2 failures all confirmed pre-existing on `main` (verified by re-running on `main`)
- [x] `grep -rln LocalExecutor` returns only historical docstring mentions; no live imports

## Remaining risks
- Tests that monkey-patch `skill_runner.subprocess.Popen` / `skill_runner.time.sleep` still work because those patches mutate the global `subprocess` / `time` module attributes, and the new `subprocess_driver.py` imports the same singletons.
- The P1.6 follow-up (returning `SkillRunResult` natively from `run_skill` and dropping the intermediate `.to_legacy_dict()` hop) is **not** in this PR — it's a wire-contract change that touches every caller and deserves its own focused review.

## Out of scope (next PRs)
Per the OMI-12 plan:
- **P1.6**: `run_skill` returns `SkillRunResult` natively
- **P2.7**: `pipelines/<name>.yaml` + generic pipeline runner (`SPATIAL_PIPELINE` becomes one config among several)
- **P2.8**: `capability_resolver` uses `registry.build_keyword_map()` inverted index; weights to module-level documented constants
- **P2.9**: golden routing test (20 representative queries → expected chosen skill)
- **P3**: structured event logging, per-skill timeouts, unified subprocess strategy

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5cbd41414f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.