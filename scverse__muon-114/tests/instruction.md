# Issue

**Title:** :sparkles: Extend _l2norm for sparse input

## Description

**Is your feature request related to a problem? Please describe.**
I tried to compute a WNN integration on a MuData object, i.e. I executed the following steps:
```
mu.pp.l2norm(mdata)
mu.pp.neighbors(mdata)
mu.tl.umap(mdata)
```
However, my Python session keeps crashing at the `l2norm` step. Omitting this step, computing neighbors and a UMAP works fine. I looked into the `mu.pp.l2norm` function and isolated the function `np.linalg.norm()` in the `_l2norm()` function as the culprit. It crashes reliably for sparse matrices.  Converting the data matrix into dense format fixes the issue. This PR extends the `_l2norm` function to sparse matrices.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31a45d76f7a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.