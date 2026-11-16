# Issue

**Title:** Refine scRNA preprocessing runtime and method validation

## Description

## Summary
- prefer the active conda environment's `Rscript` and private R library path for R-backed workflows
- keep Seurat/SCTransform preprocessing aligned with the new base-preprocessing contract (stop at PCA)
- canonicalize demo preprocessing inputs and add HVG plotting fallback for R-backed outputs
- validate and refresh method outputs for `sc-preprocessing` and `sc-clustering`

## Validation
- `45 passed, 1 skipped` for the core scRNA preprocessing/clustering test batch in the `omicsclaw` env
- direct method checks under `output/method_checks/` for:
  - `sc-preprocessing --method scanpy`
  - `sc-preprocessing --method pearson_residuals`
  - `sc-preprocessing --method seurat`
  - `sc-preprocessing --method sctransform`
  - `sc-clustering --cluster-method leiden`
  - `sc-clustering --cluster-method louvain`

## Notes
- `sctransform` still warns that `glmGamPoi` is not installed, so it runs via the slower fallback path.
- This PR was prepared from a clean worktree based on the latest `origin/main` to avoid mixing unrelated local changes from the main repo checkout.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added fallback visualization for highly variable genes with improved error handling.
  * Enhanced R environment detection across multiple installation locations.

* **Bug Fixes**
  * Improved error handling for gene visualization plotting.
  * Enhanced single-cell demo data canonicalization.

* **Changes**
  * Simplified preprocessing pipeline to focus on quality control and HVG detection.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a8880167148`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.