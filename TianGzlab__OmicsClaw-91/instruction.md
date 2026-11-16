# Issue

**Title:** feat(bot): two-tier param card for scRNA skills

## Description

## Summary

- **`_build_param_hint()` in bot/core.py**: now renders a two-tier parameter card — `核心参数` (everyday knobs) and `高级参数` (filter/threshold/algo-tuning) — with actual default values shown and an explicit LLM instruction to relay the card verbatim
- **9 scRNA SKILL.md files** split `params` into core + new `advanced_params` field: sc-markers, sc-de, sc-enrichment, sc-clustering, sc-preprocessing, sc-batch-integration, sc-pseudotime, sc-cell-communication, sc-doublet-detection

## Problem solved

Previously the LLM showed users only a simplified list of "main" parameters and silently dropped filter/threshold params (e.g. `min_fold_change`, `ora_padj_cutoff`, `n_pcs`). Users had no way to discover these without reading SKILL.md directly.

## Behavior after

Every skill result now includes a compact two-line card:
```
核心参数: groupby=leiden | n_genes=all | n_top=10
高级参数: min_fold_change=0.25 | min_in_group_fraction=0.25 | max_out_group_fraction=0.5
```

The LLM is instructed to show this verbatim, so the full parameter surface is always visible.

## Compatibility

Backward-compatible: skills without `advanced_params` render exactly as before. Spatial, genomics, proteomics, metabolomics, and bulkRNA domains are unaffected.

## Test plan

- [ ] Run sc-markers demo → verify card shows both tiers
- [ ] Run sc-clustering demo → verify n_pcs/umap_min_dist in 高级参数
- [ ] Run sc-enrichment (ora) → verify threshold params in 高级参数
- [ ] Run a spatial skill → verify output unchanged (no 高级参数 line)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Implemented two-tier parameter display system separating core parameters from advanced options for improved clarity and ease of use.

* **Refactor**
  * Reorganized parameters across single-cell analysis modules (batch integration, cell communication, clustering, differential expression, doublet detection, enrichment, marker detection, preprocessing, and pseudotime analysis) to prioritize essential parameters while marking advanced tuning options as secondary choices.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a7b6799081c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.