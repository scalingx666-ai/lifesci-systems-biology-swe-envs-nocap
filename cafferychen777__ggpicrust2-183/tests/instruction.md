# Issue

**Title:** feat(visualize_gsea): add custom color scale support; tests; CI Bioc deps

## Description

This PR adds custom color/scale support to visualize_gsea() across plot types, enabling colorblind-friendly palettes (e.g., viridis) and user-provided ggplot2 scales, while fully preserving default behavior when `scale=NULL`.

Highlights:
- New `scale` parameter in visualize_gsea() supporting:
  - color vectors (e.g., viridisLite::viridis(100))
  - palette functions (function(n) -> colors)
  - ggplot2 scale objects (scale_fill_gradientn/scale_color_gradient2, etc.)
- Unified helpers to build sequential/diverging scales and heatmap col_fun
- Heatmap respects `heatmap_params$col_fun` with highest priority; otherwise builds from `scale`, else defaults to blue-white-red
- Network uses diverging mapping (midpoint=0 for NES); barplot uses two-end colors for Positive/Negative when provided
- Added focused tests: tests/testthat/test-visualize_gsea_scale.R (forced add due to repo .gitignore). These tests pass locally.
- CI: extend setup-r-dependencies to install required deps (enrichplot, ComplexHeatmap, circlize, ggraph, tidygraph, igraph, dplyr, ggplot2) so full tests can run on CI.

Compatibility:
- Default behavior unchanged for all plot types when `scale=NULL`.
- No new hard dependencies added to DESCRIPTION; CI installs extra deps.

Next steps:
- If some matrix entries (oldrel/Windows) have Bioc install issues, we can either (a) add a dedicated Ubuntu+release test job for full tests, or (b) narrow the matrix. I can adjust based on CI results.

---
Pull Request opened by [Augment Code](https://www.augmentcode.com/) with guidance from the PR author

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `872e6bb7c328`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.