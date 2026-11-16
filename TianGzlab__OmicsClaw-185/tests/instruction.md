# Issue

**Title:** feat(pipelines): YAML-driven pipeline configs + generic chain runner (OMI-12 P2.7)

## Description

## Summary
OMI-12 P2.7 — move the spatial chain off a hard-coded `SPATIAL_PIPELINE = [...]` constant and onto YAML configs that the runtime consumes. Adding `bulkrna-pipeline` / `singlecell-pipeline` is now a one-file YAML drop-in, not a Python change with a new constant + new `_run_*_pipeline` function.

## What changes
| Path | Change |
|---|---|
| `pipelines/spatial-pipeline.yaml` | New — the existing chain expressed as data. Includes a `chain_output_basename` knob (default `processed.h5ad`) so future pipelines emitting a different baton (e.g. `counts.csv` for bulkrna) don't need a code branch. |
| `omicsclaw/core/runtime/pipeline_config.py` | New — `PipelineConfig` dataclass + `load_pipeline_config(name)` validator. Validation surfaces operator typos loudly: filename/`name:` mismatch, missing `-pipeline` suffix, empty `steps`, step without `skill`, invalid YAML — each raises `PipelineConfigError` with the file path and the failing field. |
| `omicsclaw/core/runtime/pipeline_runner.py` | Rewritten — generic `run_pipeline(config, ...)`, plus `run_pipeline_by_name(name)` that returns `None` when no YAML matches so the dispatcher can fall through to the standard "Unknown skill" path. `run_spatial_pipeline` survives as a thin compat wrapper. `SPATIAL_PIPELINE` is now derived from the YAML at import time (with a stable fallback for incomplete installs). |
| `omicsclaw/core/skill_runner.py` | Dispatcher routes any `<name>-pipeline` through `run_pipeline_by_name` first; falls through to the regular skill registry lookup when no YAML matches. |
| `omicsclaw.py` | Removed an unused duplicate `SPATIAL_PIPELINE` at module scope. |

`PIPELINES_DIR` is resolved relative to the registry's `OMICSCLAW_DIR` (env-var overridable) so wheel installs and custom layouts route pipeline lookup to the operator's data tree, matching the convention the rest of the runtime already follows.

## YAML schema
```yaml
name: spatial-pipeline                # must end with ``-pipeline`` and match the filename
description: Standard spatial...      # one-line summary
chain_output_basename: processed.h5ad # file the runner looks for in step N's output to feed step N+1
steps:
  - skill: spatial-preprocess
  - skill: spatial-domains
  ...
```

## Tests (19 new, all pass)
- `tests/test_runtime_pipeline_config.py` (13 tests) — schema validation, default chain basename, override, missing file, invalid YAML, top-level list rejection, filename/name mismatch, missing `-pipeline` suffix, empty steps, step missing `skill`, shipped spatial pipeline shape, `list_available_pipelines` discovery.
- `tests/test_runtime_pipeline_dispatch.py` (6 tests) — end-to-end chain with a stub `run_skill`: baton threading between steps, chain-basename override, failure stops chain + records partial summary, missing input produces stable error, dispatcher routes `<name>-pipeline` alias to `run_pipeline_by_name`, unknown `-pipeline` alias falls through to `Unknown skill`.

## Test plan
- [x] `pytest tests/test_runtime_pipeline_*.py tests/test_skill_runner_contract.py tests/test_output_ux.py tests/test_execution_default_executor.py tests/test_execution_executors.py tests/test_runtime_argv_builder.py tests/test_registry.py` — 69 passed, 1 skipped, 2 pre-existing env failures (`scanpy` / `fastapi`)
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_interactive_skill_run_support.py tests/test_interactive_omicsclaw_actions.py tests/test_autoagent_cli.py` — 110 passed, 2 pre-existing pydantic-version collection errors
- [x] `python omicsclaw.py list` — 89 skills × 8 domains

## Out of scope (next PRs)
- **P2.8** `capability_resolver` inverted index via `registry.build_keyword_map()`; weights → documented module constants
- **P2.9** golden routing test (20 representative queries → expected chosen skill)
- **P3** structured event logging, per-skill timeouts, unified subprocess strategy

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4c7aeb60f465`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.