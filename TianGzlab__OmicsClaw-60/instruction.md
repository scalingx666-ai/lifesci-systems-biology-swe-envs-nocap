# Issue

**Title:** Polish scRNA differential expression workflows and gallery

## Description

## Summary
- align `sc-de` with the singlecell contract by using normalized `adata.X` for exploratory DE and explicit raw-count sources for pseudobulk `deseq2_r`
- add `logreg` as an exploratory DE method and expose method-specific parameters/guidance for `logreg`, `mast`, and `deseq2_r`
- improve DE outputs with `figure_data`, effect/group summary plots, pseudobulk volcano/MA plots, and stronger upstream/downstream guidance
- fix `processed.h5ad` persistence so contracts and analysis metadata are written before save, and sync `SKILL.md`, knowhow, guide, and tests

## Validation
- `source /data/liying_environ/anaconda3_liying/bin/activate && conda activate omicsclaw && python -m pytest -q skills/singlecell/scrna/sc-de/tests/test_sc_de.py tests/test_sc_preflight.py tests/test_knowhow.py tests/test_registry.py`
- smoke outputs generated under:
  - `output/review_sc_de_wilcoxon`
  - `output/review_sc_de_logreg`
  - `output/review_sc_de_mast`
  - `output/review_sc_de_deseq2`

## Notes
- exploratory methods now assume `X = normalized_expression`; they no longer silently prefer `adata.raw`
- `deseq2_r` still focuses on pairwise contrasts, but now surfaces pseudobulk binning thresholds explicitly and reports the actual count source used
- pseudobulk smoke validation used a locally constructed raw-count test input with explicit `condition`, `sample_id`, and `cell_type` columns to exercise the full DESeq2 path

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added logistic regression (`logreg`) as a new differential expression analysis method.
  * Added configurable parameters: `--logreg-solver`, `--pseudobulk-min-cells`, `--pseudobulk-min-counts`, `--padj-threshold`, and `--log2fc-threshold`.
  * Added new visualization outputs: effect summaries, group summaries, and ranked gene panels.

* **Improvements**
  * Updated expression layer guidance—exploratory methods now use normalized expression from `adata.X`.
  * Enhanced workflow guidance for clustering prerequisites and preprocessing order.
  * Improved raw count source detection for DESeq2 analysis.

* **Documentation**
  * Updated skill documentation and guardrails with refined method-specific wording and input requirements.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `776287f594ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.