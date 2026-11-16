# Issue

**Title:** modernize test suite

## Description

Use pytest throughout instead of a unittest/pytest mixture. Also simplify some tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55a032354d9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.