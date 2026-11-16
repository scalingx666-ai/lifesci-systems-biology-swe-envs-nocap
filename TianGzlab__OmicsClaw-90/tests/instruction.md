# Issue

**Title:** fix(bot): accurate R env diagnosis when replot renders fail

## Description

## Summary

- **CLI replot**: write actual R errors to stderr (not just Python warnings to stdout) and exit code 2 when all renderers fail, so the bot subprocess can detect the real cause
- **Bot replot handler**: check both stdout+stderr for R errors; distinguish "no renderers registered" from "renderers exist but all failed"; provide actionable install commands (`conda install r-base`) instead of misleading "skill has no R Enhanced renderer"
- **Bot tool description**: explicitly list all 22 supported scRNA skills and instruct LLM to always call the tool rather than guessing whether a skill supports R Enhanced

## Context

When R is not installed, `call_r_plot()` catches the error as a Python warning (goes to stdout). The CLI exits 0 with empty stderr. The bot only checked stderr → missed the real error → told users "sc-clustering has no R Enhanced renderer" (wrong — it has 4 registered renderers). The LLM sometimes even skipped calling the tool entirely because the description was vague about which skills are supported.

## Test plan

- [ ] Test replot with R not installed → should show install command
- [ ] Test replot with R installed but missing packages → should show package install command
- [ ] Test replot with a skill that genuinely has no renderers → should list supported skills
- [ ] Test replot success path → unchanged behavior

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved detection and error messaging for missing or uninstalled R environments, now providing conda-based installation instructions.
  * Enhanced error handling and exit codes for failed renderer operations.

* **New Features**
  * Expanded R Enhanced support to 22 scRNA skill categories (previously limited subset).

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbbad672932d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.