# Issue

**Title:** Expand R Enhanced: 6 new renderers (stat, enrichment dotplot/lollipop)

## Description

## Summary
Expand R Enhanced from 14 to 20 renderers. New renderers provide publication-quality alternatives for the most common scRNA analysis figures.

### New renderers
| Renderer | Type | Used by |
|---|---|---|
| `plot_feature_violin` | Marker dotplot (summary) / Violin (cell-level) | sc-markers, sc-de |
| `plot_feature_boxplot` | Boxplot variant | (available, not wired yet) |
| `plot_cell_barplot` | Cell-type bar chart with % labels | sc-cell-annotation, sc-differential-abundance |
| `plot_cell_proportion` | Donut chart | sc-cell-annotation |
| `plot_enrichment_dotplot` | Bubble chart (gene ratio × significance) | sc-enrichment |
| `plot_enrichment_lollipop` | Stem chart (odds ratio, colored by padj) | sc-enrichment |

### Also includes
- `%||%` operator moved to common.R for shared use
- All renderers tested against real figure_data CSVs from demo runs

## Test plan
- [x] All 6 new renderers produce valid PNGs from existing figure_data
- [x] sc-cell-annotation --demo --r-enhanced: 4/4 renderers pass
- [x] sc-markers --demo --r-enhanced: 2/2 renderers pass
- [x] sc-enrichment --demo --r-enhanced (ORA): 3/3 renderers pass
- [x] Figures visually verified (dotplot, barplot, donut, lollipop)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Enrichment analysis now includes dotplot and lollipop chart visualizations for detailed results interpretation
  * Gene expression analysis supports new violin plot and boxplot options for feature visualization
  * Cell type composition visualization expanded: barplot (stacked or dodged layout) and donut chart (proportion view)
  * R-enhanced rendering pipeline enhanced across multiple modules: differential expression, cell annotation, differential abundance, enrichment, and marker analysis

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69777b4cb07b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.