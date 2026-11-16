# Issue

**Title:** Polish scRNA cell annotation workflows and guidance

## Description

## Summary
- align `sc-cell-annotation` with the singlecell skill template and updated scRNA contracts
- add explicit `manual` annotation support for user-defined cluster relabeling
- strengthen novice guidance and online-reference/model preflight prompts
- add a lightweight `knnpredict`-style reference mapping path inspired by SCOP
- update annotation galleries, figure-data exports, R reference scripts, docs, and tests

## Validation
- `python -m pytest -q skills/singlecell/scrna/sc-cell-annotation/tests/test_sc_annotate.py skills/singlecell/scrna/sc-cell-annotation/tests/test_sc_annotate_methods.py tests/test_sc_preflight.py tests/test_knowhow.py tests/test_registry.py`
- smoke outputs generated under:
  - `output/review_sc_annotation`
  - `output/review_sc_annotation_manual`
  - `output/review_sc_annotation_celltypist`
  - `output/review_sc_annotation_popv`
  - `output/review_sc_annotation_knnpredict`
  - `output/review_sc_annotation_singler_localref`
  - `output/review_sc_annotation_scmap_localref2`

## Notes
- `singler` / `scmap` using atlas keywords like `Monaco` or `HPCA` now stop in preflight and explain that `celldex / ExperimentHub` may need network access or a pre-populated cache.
- `singler` / `scmap` both support local labeled H5AD references and were validated with that path.
- `popv` currently falls back to the lightweight AnnData-first path on the bundled demo/reference combination when the official PopV path cannot satisfy its stricter raw-count/reference assumptions.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes: Single-Cell Annotation Skill Updates

* **New Features**
  * Manual cell-type annotation method with mapping file support.
  * KNNPredict lightweight reference-mapping backend.
  * CellTypist majority-voting option for improved robustness.
  * New visualization outputs: cluster-to-cell-type heatmap and cell-type count plots.

* **Improvements**
  * Enhanced cluster key resolution and auto-detection.
  * Strengthened validation and pre-flight checks for method-specific requirements.
  * Expanded reference handling for multiple annotation backends.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d50076cb042`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.