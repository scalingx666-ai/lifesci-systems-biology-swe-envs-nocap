# Issue

**Title:** 175 windows app fixes

## Description

This should fix the windows electron app.

@mase5 can you test on linux? Particularly `npm run electron` and the open loom folder button, I had to change that. Either the package updated, or it is a bit different on windows.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed3d914b015d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.