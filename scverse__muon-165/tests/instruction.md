# Issue

**Title:** DSB fixes

## Description

- make it match the R reference implementation
- implement some options that are present in the R reference implementations but were missing here

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df281ac2baac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.