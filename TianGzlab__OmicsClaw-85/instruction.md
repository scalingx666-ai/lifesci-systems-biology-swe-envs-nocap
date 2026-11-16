# Issue

**Title:** feat(singlecell): wire doublet filtering into sc-filter and sc-preprocessing

## Description

## Summary

Closes the gap where `sc-doublet-detection` only annotated cells but downstream `sc-filter` / `sc-preprocessing` never actually removed them.

- **`_lib/qc.py`** — `apply_threshold_filtering()` gains `filter_doublets=True` and `doublet_score_threshold=0.25`; removal happens between QC-threshold step and gene-filter step; `filter_stats["doublets_removed"]` propagates to all reports; silent skip when no doublet columns exist (no breaking change)
- **`sc-filter`** — new `--no-remove-doublets` / `--doublet-score-threshold` CLI flags; preflight emits guidance or `require_confirmation` depending on which column is present; report shows doublet removal status; SKILL.md updated
- **`sc-preprocessing`** — same flags; wired through `SHARED_PUBLIC_PARAM_KEYS` and `METHOD_PARAM_DEFAULTS` (all 4 methods); `prepare_preprocessing_input()` passes params down; report Summary updated; SKILL.md updated

## Preflight behaviour (Option B)

| Upstream state | Preflight action |
|---|---|
| `predicted_doublet` present | `add_guidance` — "X doublets will be auto-removed" (sc-doublet-detection already made the binary call) |
| only `doublet_score` present | `require_confirmation` — threshold is subjective; user must confirm or adjust `--doublet-score-threshold` |
| no doublet columns | `add_guidance` — suggest running `sc-doublet-detection` first |
| `--no-remove-doublets` passed | `add_guidance` — labels present but will not be used |

## Test plan

- [ ] Run `sc-doublet-detection --demo` then `sc-filter --demo` — verify `doublets_removed` appears in `filter_stats.csv` and report
- [ ] Run `sc-filter` without upstream doublet detection — verify silent skip, no error
- [ ] Pass `--no-remove-doublets` with doublet columns present — verify preflight guidance and no removal
- [ ] Pass `--doublet-score-threshold 0.1` with only `doublet_score` — verify higher removal count
- [ ] Same four cases for `sc-preprocessing`

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added automatic doublet removal during filtering when doublet detection results are available, with configurable controls
  * New flags `--no-remove-doublets` and `--doublet-score-threshold` enable users to customize doublet filtering behavior

* **Documentation**
  * Updated CLI documentation to describe automatic doublet-removal behavior and new parameters

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3158e03b12ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.