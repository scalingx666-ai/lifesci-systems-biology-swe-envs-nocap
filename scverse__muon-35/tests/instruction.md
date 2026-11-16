# Issue

**Title:** Update preproc.py

## Description

## Changes

* Simplify check for sparsity by using `scipy.sparse.issparse`

## Related issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e0988f07ae2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.