# Issue

**Title:** Harden scRNA batch integration flow and method coverage

## Description

## Summary
- strengthen `sc-batch-integration` preflight and downstream guidance toward `sc-clustering`
- add demo label support so `scanvi` can be smoke-tested reliably
- improve integration reporting and next-step metadata in `result.json` / `report.md`
- tighten the shared R bridge for batch integration, including R-side H5AD reading via `reader = "R"`
- extend method validation coverage for batch integration backends

## Validation
- `source /data/liying_environ/anaconda3_liying/bin/activate omicsclaw && python -m pytest -q skills/singlecell/scrna/sc-batch-integration/tests/test_sc_integrate.py`
  - `4 passed`
- `source /data/liying_environ/anaconda3_liying/bin/activate omicsclaw && python -m pytest -q tests/test_sc_preflight.py`
  - `27 passed`
- method smoke outputs written under `output/review_sc_batch/` for:
  - `harmony`
  - `bbknn`
  - `scanorama`
  - `scvi`
  - `scanvi`
  - `seurat_cca`
  - `seurat_rpca`
- `fastmnn` was validated on a smaller smoke input and written to `output/review_sc_batch/fastmnn_tiny`

## Notes
- `fastmnn` is still the least mature path; it now works on the smaller smoke input, but full-demo runtime is still comparatively heavy.
- This PR continues the single-cell mainline flow where preprocessing/integration/clustering are separate linked skills.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Enhanced integration diagnostics that conditionally generate based on available label information.
  * Added explicit post-integration guidance routing users to the clustering step with the correct embedding key.

* **Bug Fixes**
  * Improved batch integration handling to correctly skip integration when no meaningful batch column exists.
  * Fixed label validation for scANVI method to recognize additional label column types.

* **Documentation**
  * Updated workflow guidance to clarify integration prerequisites and recommended downstream steps.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `115ee9dfe9bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.