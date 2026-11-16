# Issue

**Title:** fix(skill-runner): drop stale SKILLS/DOMAINS snapshots (OMI-12 P0)

## Description

## Summary
Three real bugs from the OMI-12 evaluation of the route → run → execute → result-model layer:

- **Stale module-level SKILLS/DOMAINS**: `omicsclaw/core/skill_runner.py` and `omicsclaw.py` cached `SKILLS = registry.skills` / `DOMAINS = registry.domains` at import time, so `registry.invalidate()` / `registry.reload()` had no effect on the runner. Reads now go through `ensure_registry_loaded().skills` / `registry.domains`.
- **Missing `import json` in `executors/default.py`**: `_coerce_param_value` raised `NameError` for list/dict-typed params like `--resolutions [0.4, 0.6, 0.8]`.
- **Private-field poking in `bot/skill_orchestration._lookup_skill_info`**: replaced `skill_registry._loaded = False` / `skills.clear()` / `lazy_skills.clear()` with the public `registry.reload()`.

## Why
Pre-fix repro for the stale cache (from the OMI-12 body):
```
python -c "from omicsclaw.core import skill_runner; from omicsclaw.core.registry import registry; registry.invalidate(); print(len(skill_runner.SKILLS), len(registry.skills))"
175 0   ← stale snapshot
```
After fix:
```
python -c "from omicsclaw.core import skill_runner; from omicsclaw.core.registry import registry; registry.invalidate(); print(len(registry.skills)); skill_runner.resolve_skill_alias('spatial-preprocess'); print(len(registry.skills))"
0
175   ← runner re-loads via ensure_registry_loaded()
```

## New tests
- `test_registry::test_skill_runner_sees_registry_invalidate_after_load` — runner re-loads via `ensure_registry_loaded()` after `invalidate()`.
- `test_registry::test_registry_reload_clears_stale_entries_for_runner` — `reload()` clears synthetic stale entries from the runner's read.
- `test_execution_default_executor::test_default_command_factory_serialises_list_and_dict_params` — list & dict params round-trip through `json.dumps`.

Updated: `test_skill_runner_contract.py` / `test_output_ux.py` now patch the live registry instead of the removed module globals.

## Test plan
- [x] `python omicsclaw.py list` — 89 skills × 8 domains
- [x] `pytest tests/test_registry.py tests/test_skill_runner_contract.py tests/test_output_ux.py tests/test_execution_default_executor.py` — 29/31 pass (2 pre-existing env failures: missing `scanpy` and `fastapi`)
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py` — 97 passed (2 pre-existing pydantic-version collection errors unrelated to this PR)
- [x] `pytest tests/test_registry_alias_contract.py tests/test_registry_skills_snapshot.py tests/test_registry_discovery.py tests/test_registry_lazy.py` — 20/20

## Remaining risks
- The runner now calls `registry.load_all()` per public-function entry. That is the documented cached path (idempotent on `self._loaded`), so it costs one dict-equality check, not a disk scan.
- Module-level `SPATIAL_PIPELINE` constant unchanged — that is P2 in the OMI-12 eval (data-driven pipelines).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Fixed runtime failures when passing non-primitive parameter values (lists, dictionaries) to commands by implementing proper JSON serialization support.

* **Performance Improvements**
  * Skills and domain metadata are now loaded on-demand instead of eagerly at application startup, reducing initial load time.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/181)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b9afed9b69f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.