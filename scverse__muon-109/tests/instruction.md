# Issue

**Title:** Fix save color in MuData

## Description

Fixes a regression introduced in 19f98d2ef80463b7e691b5b69030158838ec216b.
The problem is that for continuous variables, no color
gets stored in AnnData, therefore plotting continuous variables with
muon fails at the moment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae15b5001c38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.