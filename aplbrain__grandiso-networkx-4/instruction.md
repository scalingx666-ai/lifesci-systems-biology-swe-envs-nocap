# Issue

**Title:** Add count interface

## Description

By passing `count_only=True`, the user will avoid the additional memory overhead of collecting and storing mappings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c24b0a52e12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.