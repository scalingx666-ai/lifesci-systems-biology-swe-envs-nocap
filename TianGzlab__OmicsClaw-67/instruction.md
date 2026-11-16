# Issue

**Title:** Fix sc-cell-annotation all-Unknown bug and add UX templates

## Description

## Summary

- **Fix critical bug**: markers method returned all "Unknown" for non-PBMC data due to hardcoded 5-type PBMC markers with silent gene-mismatch skip
- **Fix cold-start crash**: removed `NUMBA_DISABLE_JIT=1` from shared `_lib` modules that corrupted numba after scanpy import, causing `AttributeError` on first run
- **Add UX guardrail templates**: codified user experience rules for all future skill reviews

## Changes

### sc-cell-annotation fixes (core)
- Expand built-in markers: 5 PBMC → 21 multi-tissue (blood, brain, epithelial, stromal)
- New `--marker-file` flag: users can provide custom markers in JSON/CSV
- Species auto-detection: human (UPPERCASE) vs mouse (Title case) with case-insensitive rescue
- Gene overlap diagnostics: 0% / <30% / normal — graduated warnings
- All-Unknown detection with 3 fix options printed to stdout
- `report.md` dynamic Troubleshooting section
- `result.json` adds `annotation_diagnostics` for bot/agent
- popv/knnpredict errors now include download URLs + alternative methods
- SKILL.md Reference Data Guide: method selection table, CellTypist models, reference sources

### numba cold-start crash fix
- Remove `os.environ.setdefault("NUMBA_DISABLE_JIT", "1")` from `_lib/__init__.py`, `_lib/adata_utils.py`, `sc_cell_communication.py`
- Use `ensure_runtime_cache_dirs()` for unified cache management

### New templates
- `SC-USER-EXPERIENCE-RULES.md`: 7 rules for input detection, failure guidance, reference data, defaults, fallbacks, method selection
- `SC-DEVELOPMENT-CHECKLIST.md`: +14 items (Runtime Environment + User Experience sections)
- `SC-SKILL-TEMPLATE.md`: runtime env requirements + 6 new anti-patterns

## Test plan

- [x] 434 existing tests pass (1 pre-existing unrelated failure)
- [x] 52 annotation/preflight tests pass
- [x] Demo mode cold-start: 6 cell types, 0 Unknown on pbmc3k
- [x] Unit tests: human genes, mouse genes (case rescue), fake genes (all Unknown + warning), custom marker file
- [x] Species detection: human=UPPER, mouse=Title case

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  - Added `--marker-file` parameter to support custom marker files for cell annotation.
  - Implemented case-insensitive gene name matching for improved cross-species compatibility.

* **Improvements**
  - Enhanced error messages to include download links and alternative annotation methods.
  - Added troubleshooting guidance for cells labeled as "Unknown" with actionable fixes.
  - Improved gene-overlap diagnostics and organism detection.

* **Documentation**
  - Expanded skill guides with reference data selection guidance and method comparison tables.
  - Added reference requirements and troubleshooting sections to knowledge base.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1025424c86ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.