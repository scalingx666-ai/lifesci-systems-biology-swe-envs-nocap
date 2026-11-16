# Issue

**Title:** FIX: replace `scanpy.neighbors._compute_connectivities_umap` with `sc…

## Description

…anpy.neighbors._connectivity.umap`

Scanpy 1.10.0+ removes `scanpy.neighbors._compute_connectivites_umap`, but the required functionality is still provided by `scanpy.neighbors._connectivity.umap`, so this PR swaps those out.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61942d63bae0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.