# Issue

**Title:** Indicate tested comparison or covariate in test output

## Description

Before it was somewhat hard to figure out what specific comparison the log-fold changes and p-values corresponded to.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47b5f7fcab94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.