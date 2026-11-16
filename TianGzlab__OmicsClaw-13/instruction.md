# Issue

**Title:** fix: Improve spatial skills with bug fixes and naming consistency

## Description

## Summary

- **Memory leak prevention**: Add `plt.close('all')` after figure generation across all 12 spatial scripts to prevent matplotlib figure accumulation
- **Skill naming consistency**: Standardize skill names in orchestrator and README to match full canonical names (e.g., `preprocess` → `spatial-preprocessing`, `integrate` → `spatial-integration`)
- **Bug fixes**: Fix Harmony/Scanorama integration, PASTE registration coordinate transform, CellRank 2 macrostates lookup, VELOVI layer setup, gseapy result attribute access, importlib fallback errors
- **Dependency modernization**: Replace deprecated `pkg_resources` with `importlib.metadata` in spatial-integrate and spatial-register
- **Parameter tuning**: Adjust inferCNVpy defaults (window_size: 250→100, step: 50→10) for better resolution
- **Resource cleanup**: Use `TemporaryDirectory` context manager in spatial-statistics demo

## Test plan

- [ ] Run `python omicsclaw.py run spatial-preprocessing --demo` to verify preprocessing still works
- [ ] Run `python omicsclaw.py run spatial-de --demo` to verify DE analysis
- [ ] Run `python omicsclaw.py list` to verify updated skill names display correctly
- [ ] Verify no matplotlib memory warnings in long-running sessions

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d31b46ca8f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.