# Issue

**Title:** feat(runtime): result.json status field + safe fallback to -9→0 heuristic (OMI-12 audit P1 #2)

## Description

## Summary
OMI-12 audit 🟡 P1 #2 — move the runner's success/failure decision off the brittle ``-9 + result.json exists → success`` SIGKILL heuristic onto an explicit signal the skill emits. The legacy heuristic stays as a fallback so the 89 existing skills don't have to migrate at once.

## The contract

| Side | API | Behaviour |
|---|---|---|
| Skill (last line) | `mark_result_status(output_dir, "ok"\|"partial"\|"failed")` | Patches `result.json` with a top-level `status` field. Rejects unknown values; never raises. |
| Runner | `read_result_status(out_dir)` consumed inside `drive_subprocess` | When present, overrides exit code: `"ok"` → 0; `"partial"` / `"failed"` → flips zero to 1 (preserves any non-zero). When absent → falls back to the existing `-9 → 0` heuristic. |
| Cancel | always wins | Regardless of any status the partial `result.json` carries; the user's explicit abort is decisive. |

## What changes

| File | Change |
|---|---|
| `omicsclaw/common/report.py` | New `mark_result_status` + `read_result_status` helpers with the documented taxonomy. |
| `omicsclaw/core/runtime/subprocess_driver.py` | `drive_subprocess` reads the status field first; the `-9 → 0` heuristic survives unchanged in the `else` branch. Docstring updated. |
| `templates/skill/replace_me.py` | Tail-calls `mark_result_status(args.output, "ok")` with a comment explaining why "last step" matters (a crash before that line leaves the field absent and the legacy heuristic stays in charge). |
| `templates/skill/references/output_contract.md` | Documents the status field and taxonomy for skill authors copying the template. |

### Why "last step" matters

If a skill writes `result.json` during normal flow then crashes, a defaulted `status: "ok"` would falsely report success for a crashed run. The contract — and the template — require the skill to mark status **after** every other write has succeeded. A crash before that point leaves the field absent, and the runner falls back to its exit-code logic.

### Why this is safe for the 89 existing skills

None of them emit a status field yet, so `read_result_status` returns `None` and the runner uses the unchanged legacy path. Migration is opt-in, one line at the bottom of each skill script.

## New tests (12)
`tests/test_result_status_contract.py` covers:
- `mark_result_status` writes / rejects unknown values / returns False when envelope missing
- `read_result_status` returns None for absent or off-taxonomy values
- `status=ok` overrides non-zero exit
- `status=failed` / `partial` overrides zero exit; preserves existing non-zero
- Missing status falls back to the legacy `-9 + result.json` heuristic
- Cancellation overrides `status=ok` (uses `signal.SIG_IGN` on SIGTERM to force the SIGKILL escalation path)

## Test plan
- [x] `pytest tests/test_result_status_contract.py` — **12 / 12 pass**.
- [x] `pytest tests/test_skill_runner_contract.py tests/test_output_ux.py tests/test_execution_default_executor.py tests/test_execution_executors.py tests/test_runtime_*.py tests/test_registry.py tests/test_capability_resolver*.py tests/test_routing_regression.py tests/test_bot_n_epochs_routing.py tests/test_result_status_contract.py` — 127 passed, 2 skipped, 5 xfailed; 2 pre-existing env failures unrelated (`scanpy` / `fastapi`).
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_bot_runner_contract.py tests/test_interactive_omicsclaw_actions.py` — 104 passed; same 4 pre-existing failures as `main`.
- [x] `pytest templates/skill/tests/` — 2 / 2 pass.
- [x] `python templates/skill/replace_me.py --demo --output /tmp/smoke` — `result.json` carries `"status": "ok"`.
- [x] `python omicsclaw.py list` — 89 skills × 8 domains.

## Follow-up
The 89 already-shipped skills can migrate one at a time by adding the tail call at the bottom of their script. Once enough have migrated, a future PR can drop the legacy `-9 → 0` heuristic entirely.

## Remaining backlog
- **🟡 P1 #4** — Converge `SkillRunnerExecutor` onto `SubprocessExecutor` (~1 day; eliminates the `asyncio.to_thread`-wrapped blocking Popen that exhausts the default ThreadPoolExecutor under multi-user load).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f2a3ec7e5b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.