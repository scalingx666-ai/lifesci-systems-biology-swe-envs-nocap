# Issue

**Title:** Phase 20: Enhance existing R Enhanced renderers (+5 new)

## Description

## Summary

Phase 20 of the R Enhanced Gallery milestone — enhance existing renderers with advanced scop features.

### New Renderers (+5, total 30→35)

| Renderer | R File | scop Equivalent |
|----------|--------|-----------------|
| `plot_enrichment_network` | enrichment.R | EnrichmentPlot network mode |
| `plot_enrichment_enrichmap` | enrichment.R | EnrichmentPlot enrichmap mode |
| `plot_de_manhattan` | de.R | DEtestPlot manhattan mode |
| `plot_ccc_bipartite` | communication.R | CCCNetworkPlot bipartite mode |
| `plot_ccc_diff_network` | communication.R | CCCNetworkPlot diff mode |

### Enhanced Renderer (in-place upgrade)

| Renderer | Enhancement |
|----------|-------------|
| `plot_pseudotime_dynamic` | Multi-lineage support — detects "lineage" column, facets per lineage with separate loess curves. Fully backward compatible. |

### Python Wiring
- sc-enrichment: R_ENHANCED_SHARED +2 entries (network, enrichmap)
- sc-de: R_ENHANCED_PLOTS +1 entry (manhattan)
- sc-cell-communication: R_ENHANCED_PLOTS +2 entries (bipartite, diff_network)

### Dependencies
- `igraph` R package: used by enrichment network/enrichmap (guarded with requireNamespace, graceful fallback)

## Test plan
- [x] All R files follow `function(data_dir, out_path, params)` contract
- [x] registry.R has 35 registered renderers (no duplicates)
- [x] No .planning files in git tracking
- [ ] Run `--demo --r-enhanced` on sc-enrichment, sc-de, sc-cell-communication

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added cell communication visualizations: bipartite plot for ligand-receptor interactions and differential network plot for condition comparisons
  * Added differential expression Manhattan plot for marker gene visualization
  * Added enrichment analysis visualizations: network plot and enrichment map with similarity clustering
  * Enhanced pseudotime dynamic plots to support multi-lineage comparisons with flexible display modes

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0aa91b6e4bb1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.