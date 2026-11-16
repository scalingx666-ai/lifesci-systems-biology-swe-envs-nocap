# Issue

**Title:** R Enhanced expansion: DynamicHeatmap + wider skill coverage

## Description

## Summary
- New `plot_pseudotime_heatmap` renderer (DynamicHeatmap equivalent): gene expression binned along pseudotime, z-scored, ordered by peak position
- Embedding renderers now accept multiple CSV formats (coord1/coord2, UMAP_1/UMAP_2, dim1/dim2) and auto-detect continuous features
- Expanded R_ENHANCED_PLOTS in 10 skills — most skills now have 3-5 renderers instead of just 1-2

### Coverage summary (21 renderers → 19 skills)
| Skill | Before | After |
|---|---|---|
| sc-pseudotime | 2 | **5** (lineage, dynamic, heatmap, embedding×2) |
| sc-cell-annotation | 4 | 4 |
| sc-de | 3 | 3 |
| sc-markers | 2 | 2 |
| sc-enrichment | 3-5 | 3-5 |
| sc-velocity | 1 | **3** |
| sc-clustering | 2 | **4** |
| sc-metacell | 1 | **3** |
| Others (qc, doublet, grn, etc.) | 1-2 | **2-3** |

## Test plan
- [x] pseudotime --demo --r-enhanced: 5/5 renderers pass
- [x] DynamicHeatmap figure quality verified (z-score heatmap with Early/Mid/Late axis)
- [x] Embedding renderers work with pseudotime CSV format (coord1/coord2 + Inf filtering)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added pseudotime heatmap visualization showing gene expression across pseudotime intervals.
  * Embedding plots now support alternative coordinate naming conventions (coord1/coord2, UMAP_1/UMAP_2).
  * Improved feature auto-detection in embedding plots with expanded candidate column names.
  * Expanded R-enhanced plotting across multiple analysis workflows.

* **Bug Fixes**
  * Enhanced numeric handling in embedding plots (Inf/-Inf converted to NA).

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9580eb843d39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.