# Issue

**Title:** Polish scRNA doublet detection methods and gallery

## Description

## Summary
- expand `sc-doublet-detection` with `doubletdetection` and `scds`
- reuse shared raw-count source selection and preserve AnnData matrix semantics
- add richer doublet figures, figure-data exports, and stronger novice guidance
- align `SKILL.md`, knowhow, skill-guide, registry, and dependency metadata

## Validation
- `python -m pytest -q skills/singlecell/scrna/sc-doublet-detection/tests/test_sc_doublet.py tests/test_scrna_method_contracts.py tests/test_sc_preflight.py tests/test_knowhow.py tests/test_registry.py`
- smoke outputs generated under:
  - `output/review_sc_doublet_scrublet`
  - `output/review_sc_doublet_doubletdetection`
  - `output/review_sc_doublet_doubletfinder`
  - `output/review_sc_doublet_scdblfinder`
  - `output/review_sc_doublet_scds`
  - `output/review_sc_doublet_scds_hybrid`

## Notes
- `scds --scds-mode hybrid` currently falls back to `cxds` in the active environment because the bundled `bcds` path is not compatible with the installed xgboost stack; the wrapper reports this honestly in `report.md` and `result.json`.
- runtime behavior still only **prompts** for missing optional dependencies; it does not auto-install them for end users.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added DoubletDetection and scds methods (configurable modes), batch-key support, and CSV export of doublet calls
  * New visual outputs: score distribution, call summary, embedding and group-comparison plots

* **Documentation**
  * Expanded doublet detection guide and pre-run/run guidance; clarified expected-rate semantics and that annotation does not remove cells
  * Updated “what to inspect” and recommended next steps after running

* **Chores**
  * Added optional dependencies for the new methods
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c7b29ac79c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.