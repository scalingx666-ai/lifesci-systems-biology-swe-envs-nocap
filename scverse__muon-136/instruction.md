# Issue

**Title:** scanpy 1.10 compat + PR CI

## Description

- FIX: replace `scanpy.neighbors._compute_connectivities_umap` with `scanpy.neighbors._connectivity.umap`
- Change for black
- fix for `_choose_representation` arguments
- update CI to run on PRs
- release note

.

Changes proposed in this pull request:
- 
- 
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61942d63bae0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.