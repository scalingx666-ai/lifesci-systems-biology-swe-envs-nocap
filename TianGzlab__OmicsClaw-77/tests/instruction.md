# Issue

**Title:** fix: R Enhanced full coverage (43 renderers) + primary method validation (liana/SEACells/cNMF)

## Description

## Summary

- **R Enhanced rendering tested on all 22 skills** with real data — 43 PNGs generated successfully
- **Fixed feature_cor gap**: sc-de now exports `gene_expression.csv` for the correlation renderer
- **Fixed R renderer bugs**: embedding.R empty column crash, UMAP coordinate normalization, 11 skills' R_ENHANCED_PLOTS mismatches
- **Validated 3 primary methods**: liana (2447 L-R pairs), SEACells (50 metacells), cNMF (10 programs)

## R Enhanced Fixes

| Fix | File |
|---|---|
| Add gene_expression.csv export for feature_cor | sc_de.py |
| Fix empty num_cols sapply crash | embedding.R |
| UMAP coordinate normalization for R renderers | embedding.R |
| Remove wrong renderer assignments at pre-clustering stages | 11 skill .py files |

## Primary Method Validation

| Method | Package | L-R Pairs / Metacells / Programs | Status |
|---|---|---|---|
| liana | 1.7.1 | 2447 pairs, 541 significant | PASS |
| SEACells | 0.3.3 | 50 metacells, 6-10 iter convergence | PASS |
| cNMF | 1.7.1 | 10 programs, biologically coherent | PASS |

## Test plan

- [x] 43 R Enhanced PNGs across 19 skills verified
- [x] feature_cor renderer now works (was broken)
- [x] liana tested with real PBMC data (not fallback builtin)
- [x] SEACells tested with real PBMC data (not fallback kmeans)
- [x] cNMF tested with real PBMC data (not fallback NMF)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Enhanced support for additional embedding data formats (Cytotrace and UMAP).
  * Gene expression CSV export now available across multiple analysis workflows for improved visualization and downstream analysis.
  * Additional summary data exports including cell type counts and embedding point coordinates.

* **Updates**
  * Refined R-based visualization renderers across single-cell workflows for better feature-focused analysis.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7651c6842ae4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.