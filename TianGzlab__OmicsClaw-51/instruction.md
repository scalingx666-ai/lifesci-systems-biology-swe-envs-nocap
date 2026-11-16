# Issue

**Title:** Harden scRNA upstream backend validation paths

## Description

## Summary
This PR hardens the scRNA upstream validation paths on top of the latest `main`.

Key fixes:
- fix FastQC/MultiQC real-path execution in `sc-fastq-qc`
- fix STARsolo output prefix/path handling in `sc-count`
- improve pseudoalign backend wrappers and artifact detection for `kb_python` and `simpleaf`
- improve tiny-input robustness for `sc-velocity` and STARsolo velocity import handling
- improve barcode-rank plotting fallback for zero-count edge cases

## What was validated
Real or near-real method validation outputs were generated under:
- `output/skill_method_checks_scrna_upstream/sc-fastq-qc/real_fastqc`
- `output/skill_method_checks_scrna_upstream/sc-count/cellranger_real`
- `output/skill_method_checks_scrna_upstream/sc-count/starsolo`
- `output/skill_method_checks_scrna_upstream/sc-count/kb_python_valid`
- `output/skill_method_checks_scrna_upstream/sc-count/simpleaf_valid`
- `output/skill_method_checks_scrna_upstream/sc-velocity-prep/velocyto_bam`
- `output/skill_method_checks_scrna_upstream/sc-velocity-prep/starsolo_v2`
- `output/skill_method_checks_scrna_upstream/sc-velocity/stochastic`
- `output/skill_method_checks_scrna_upstream/sc-velocity/steady_state`
- `output/skill_method_checks_scrna_upstream/sc-velocity/dynamical`

## Test
- `pytest skills/singlecell/scrna/sc-fastq-qc/tests/test_sc_fastq_qc.py skills/singlecell/scrna/sc-count/tests/test_sc_count.py skills/singlecell/scrna/sc-velocity-prep/tests/test_sc_velocity_prep.py skills/singlecell/scrna/sc-velocity/tests/test_sc_velocity.py -q`
- result: `18 passed`

## Notes
Not included in this PR:
- `emit-bam` / keep-BAM user interaction for future velocity planning
- larger production-scale dataset validation beyond the current real/tiny backend checks

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added support for kb-python reference formats and expanded simpleaf compatibility
  * Enhanced robustness for small datasets, preventing analysis failures

* **Bug Fixes**
  * Fixed visualization crashes with empty barcode data
  * Improved sparse matrix handling in velocity analysis
  * Enhanced fallback mechanisms for data loading edge cases
  * Corrected path handling for analysis workflows

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a8880167148`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.