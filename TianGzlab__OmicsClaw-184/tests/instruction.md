# Issue

**Title:** refactor(skill-runner): run_skill returns SkillRunResult natively (OMI-12 P1.6)

## Description

## Summary
OMI-12 P1.6 — flip `run_skill` to return `SkillRunResult` natively. Previously the runner did `build_skill_run_result(...).to_legacy_dict()` and every consumer ran `coerce_skill_run_result(result)` to convert back. This PR eliminates that wasteful dict↔model round-trip.

## Runner-side
- `run_skill` annotation + return: `SkillRunResult` (was `dict`).
- `_err` annotation + return: `SkillRunResult`.
- `run_spatial_pipeline`: same; internal loop switched from `result["success"]` / `result.get("method")` to attribute access.
- `result_json_fallback`: falls back to `result.to_legacy_dict()` when `result.raw` is empty (the new common case — natively built results don't carry a captured raw mapping).

## Consumer migrations
| File | Change |
|---|---|
| `omicsclaw/execution/executors/default.py` | Drop the `coerce_skill_run_result(result)` step; assign the runner's return directly. |
| `bot/skill_orchestration._run_skill_via_shared_runner` | Same — drop the coerce. |
| `omicsclaw.py` CLI | `result["success"]` etc. → `result.success` attribute access. |
| `omicsclaw/agents/tools.py` | Same. |
| `omicsclaw/interactive/_omicsclaw_actions.py` | `run_skill_command` adds `.to_legacy_dict()` at the boundary so the existing `build_skill_run_display_view` dict consumers stay untouched. |

## Test migrations
- `test_skill_runner_contract.py` — dict→attribute access; **new** `test_run_skill_returns_skill_run_result_natively` pin test locking in the typed return for the error path.
- `test_output_ux.py` — same dict→attribute migration for the end-to-end assertion.
- `test_execution_default_executor.py`, `test_bot_runner_contract.py`, `test_autoagent_cli.py` — `fake_run_skill` mocks now return `build_skill_run_result(...)` so the executor / bot adapter sees the new contract.
- `test_interactive_omicsclaw_actions.py` — mock returns the typed model; the assertion still validates the dict shape since `run_skill_command` translates at the boundary.

`coerce_skill_run_result` stays public — still useful for callers that receive runner-shaped data from external sources (RPC, persisted fixtures) and need a model.

## Test plan
- [x] `pytest tests/test_skill_runner_contract.py tests/test_output_ux.py tests/test_execution_default_executor.py tests/test_execution_executors.py tests/test_runtime_argv_builder.py tests/test_registry.py tests/test_autoagent_cli.py tests/test_interactive_omicsclaw_actions.py tests/test_bot_runner_contract.py tests/test_skill_run_result.py` — 63 passed, 1 skipped, 4 pre-existing env failures (scanpy / fastapi missing; bot logger-name assertion mismatch — all confirmed pre-existing on main)
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_interactive_skill_run_support.py` — 102 passed, 2 pre-existing pydantic-version collection errors
- [x] `python omicsclaw.py list` — 89 skills × 8 domains
- [x] `grep -rln coerce_skill_run_result` — only the function definition + a test that exercises the coerce path directly remain; no consumer round-trip

## Remaining backlog
Per the OMI-12 plan:
- **P2.7** `pipelines/<name>.yaml` + generic pipeline runner (`SPATIAL_PIPELINE` becomes one config among several)
- **P2.8** `capability_resolver` uses `registry.build_keyword_map()` inverted index; weights to module-level documented constants
- **P2.9** golden routing test (20 representative queries → expected chosen skill)
- **P3** structured event logging, per-skill timeouts, unified subprocess strategy

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe4cf5bf37bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.