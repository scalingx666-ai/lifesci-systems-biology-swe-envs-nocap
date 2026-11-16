# Issue

**Title:** Feat / seurat flavored clr

## Description

## Changes

* Adds argument `axis` to `muon._prot.preproc.py:clr` to apply CLR across the specified axis.
* Sparse matrices are no longer densified.
* CLR normalization is inplace, i.e. variable assignments are kept at a minimum.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dae9e94d77a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.