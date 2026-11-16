# Issue

**Title:** docs: clarify plotting keyword arguments

## Description

.

This clarifies that additional keyword arguments in `mu.pl.scatter` and `mu.pl.embedding` are passed through to the corresponding Scanpy plotting functions.

Tests are not required because this is a documentation-only change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e70cc20071ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.