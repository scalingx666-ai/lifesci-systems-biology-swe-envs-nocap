# Issue

**Title:** feat(bot): add replot_skill for R Enhanced re-rendering in bot/oc-chat

## Description

## Summary

- Add `replot_skill` ToolSpec in `omicsclaw/runtime/bot_tools.py` — exposes `skill`, `output_path`, `renderer` (optional), `return_media` (default `all`), and full plot-param suite (`top_n`, `font_size`, `dpi`, `palette`, `title`, `width`, `height`)
- Add `execute_replot_skill` async executor in `bot/core.py` — validates `output_path` / `figure_data/` existence, builds the `omicsclaw.py replot` subprocess, collects figures from `figures/r_enhanced/`, queues them in `pending_media` for delivery
- Register `replot_skill` in `_available_tool_executors()`

## Behaviour

| Turn | User says | Bot calls |
|------|-----------|-----------|
| 1 | "run sc-qc on my file" | `omicsclaw(skill='sc-qc', ...)` → Python figures |
| 2 | "re-draw with R" | `replot_skill(skill='sc-qc', output_path='...')` → R Enhanced figures delivered |

Only scRNA skills have `R_ENHANCED_PLOTS`; other domains return a friendly "not supported" message — zero impact on existing skill runs or first-round Python plots.

## Test plan

- [ ] Run `sc-qc --demo`, then ask bot "用R重画" — verify `r_qc_violin.png` delivered
- [ ] Ask bot to replot a spatial skill — verify friendly "not supported" message returned
- [ ] Pass `--renderer plot_feature_violin` via `extra_args` — verify only that renderer runs

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added replot_skill tool for re-rendering previously generated plots from skill runs.
  * Supports customization options: font size, dimensions (width/height), color palette, DPI, title, and figure filtering.
  * Includes optional renderer selection for flexible output rendering.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3158e03b12ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.