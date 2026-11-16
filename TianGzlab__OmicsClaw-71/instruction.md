# Issue

**Title:** R Enhanced: CCC bubble matrix + 3 more skills (22/29 coverage)

## Description

## Summary
- New `plot_ccc_bubble` renderer: ligand-receptor bubble matrix (scop CCCHeatmap bubble equivalent)
- R Enhanced support added to 3 previously unsupported skills: sc-ambient-removal, sc-filter, sc-in-silico-perturbation
- Registry: 22 renderers, 22/29 skills now have R Enhanced

### New renderer
| Renderer | Description | Skill |
|---|---|---|
| `plot_ccc_bubble` | L-R pairs × cell pairs bubble matrix (size=score, color=significance) | sc-cell-communication |

### Newly supported skills
| Skill | Renderers |
|---|---|
| sc-ambient-removal | embedding_discrete, embedding_feature |
| sc-filter | feature_violin, cell_barplot |
| sc-in-silico-perturbation | embedding_discrete, embedding_feature |

### Remaining 7 skills without R Enhanced
sc-count, sc-multi-count, sc-fastq-qc, sc-drug-response, sc-perturb-prep, sc-standardize-input, sc-velocity-prep — all are upstream/utility skills where R Enhanced adds minimal value.

## Test plan
- [x] plot_ccc_bubble renders valid PNG from CCC figure_data
- [x] sc-cell-communication --demo --r-enhanced: 3/3 renderers pass
- [x] sc-ambient-removal --demo --r-enhanced: runs (embedding warns gracefully — expected, no embedding CSV exported)
- [x] CCC bubble figure quality verified

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added bubble matrix visualization to display ligand-receptor interaction patterns.
  * Added optional `--r-enhanced` flag to enable enhanced R-based figure generation across multiple analysis workflows.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `273002d8bca3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.