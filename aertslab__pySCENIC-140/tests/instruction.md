# Issue

**Title:** GRN multiprocessing and sparse matrix support

## Description

Updates:
* Added a helper script `scripts/arboreto_with_multiprocessing.py` that runs the Arboreto GRN algorithms (GRNBoost2, GENIE3) without Dask for compatibility.
* Initial support for the use of sparse expression matrices (applies only to the GRN step in the CLI currently). Using sparse matrices with the GRN step requires a patch to Arboreto ()

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bee25764bbe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.