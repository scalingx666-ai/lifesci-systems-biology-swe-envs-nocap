# Issue

**Title:** Fix scRNA bugs and optimize R Enhanced rendering

## Description

## Summary
- Fix sc-differential-abundance pandas CategoricalIndex crash in demo mode
- Fix R Enhanced rendering: viridis fallback, ORA/GSEA method-aware renderers, CCC network self-loop fix
- Wire --gsea-min-size/--gsea-max-size CLI args through to R scripts (were disconnected)
- Auto-fallback for optional dependencies: cnmf→nmf, seacells→kmeans

## Test plan
- [x] sc-differential-abundance --demo (milo, simple, proportion_test_r)
- [x] R Enhanced: DE volcano+heatmap, enrichment bar, CCC heatmap+network, pseudotime lineage+dynamic
- [x] sc-gene-programs --demo auto-fallback to nmf
- [x] sc-metacell --demo auto-fallback to kmeans
- [x] Chain test: annotation → markers with real h5ad output
- [x] Core skills: annotation, markers, pseudotime, DE, enrichment, GRN, ambient, perturb-prep, in-silico-perturbation, standardize-input

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added configurable minimum and maximum gene set size parameters for GSEA and GSVA enrichment analyses.

* **Improvements**
  * Enhanced network visualization by excluding self-loop edges in communication plots.
  * Added graceful fallback to alternative methods (NMF, k-means) when optional dependencies are unavailable.
  * Made viridis color palette loading conditional for improved flexibility.

* **Bug Fixes**
  * Fixed index handling in differential abundance calculations to prevent downstream errors.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bf05925a7b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.