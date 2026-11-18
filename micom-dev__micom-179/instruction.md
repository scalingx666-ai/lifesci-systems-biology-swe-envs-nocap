# Issue

**Title:** Some small fixes

## Description

Fixes the CI on MacOS by reverting to non-ARM.

 .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20eb6e0a868d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.