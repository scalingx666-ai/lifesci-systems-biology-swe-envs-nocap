# Issue

**Title:** Fix regression in b855e9d

## Description

This fixes a regression introduced in b855e9d whereby an `image` variable is not in scope which crashes the application.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eef083a149c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.