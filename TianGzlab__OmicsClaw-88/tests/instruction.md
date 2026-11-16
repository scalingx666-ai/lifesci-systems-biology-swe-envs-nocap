# Issue

**Title:** fix(bot): prevent LLM fallback chain when replot fails

## Description

## Summary
- When R Enhanced rendering silently fails (exit 0 but no PNG), detect R package errors in stderr and return actionable `Rscript -e 'install.packages(...)'` commands
- Add `"there is no package called"` to `_ENV_ERROR_PATTERNS` so R package errors get the same structured UX as Python/NumPy errors
- Add anti-fallback instruction to `replot_skill` tool description — LLM now relays errors directly instead of cascading through custom_analysis_execute → rpy2 → seaborn

## Problem
When a user asked the bot to "use R Enhanced to redraw", `replot_skill` would return a vague "no R Enhanced figures were generated" message. The LLM then improvised a degradation chain (custom_analysis_execute → rpy2 → Python/seaborn → give up), which was confusing and unhelpful.

## Test plan
- [ ] Run `replot sc-qc` on an output dir with figure_data but missing R packages — should return structured error with install command
- [ ] Run `replot sc-qc` on an output dir with working R environment — should produce R Enhanced figures as before
- [ ] Verify LLM does not fall back to custom_analysis_execute when replot returns an error

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82e897846f78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.