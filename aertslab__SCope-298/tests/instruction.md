# Issue

**Title:** Speed up server CI

## Description

Removes dependency on the pre-packaged github action for poetry.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bca20e8a02b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.