# Issue

**Title:** Fix prot.pp.clr for old-style sparse matrices

## Description

### Problem

`muon.prot.pp.clr` crashes on the seurat flavor when `adata.X` is an old-style SciPy sparse matrix (`csc_matrix` / `csr_matrix`):

```python
mu.prot.pp.clr(adata, axis=1)
# AttributeError: 'matrix' object has no attribute 'toarray'
```

For an `spmatrix`, `np.log1p(x).mean(axis=axis)` returns a `numpy.matrix`, which has no `.toarray()` method, so the existing line fails. This affects common datasets whose ADT `.X` is still an `spmatrix` (e.g. `papalexi_2021`).

### Fix

Compute the per-feature log-mean once and coerce it to a plain array depending on the container type:

- old-style `csc_matrix` / `csr_matrix`: use `.A` and `x.getnnz(axis=axis)`
- sparse arrays: use `np.diff(x.indptr)` to avoid the `getnnz` behavior change (scipy/scipy#19405)

The `axis` type hint is also tightened to `Literal[0, 1]`.

### Verification

Installed this branch and ran the pertpy `perturbation_efficacy` tutorial (which calls `mu.prot.pp.clr(mdata["adt"], axis=1)` on `papalexi_2021`) end-to-end: all 32 code cells execute with no errors. CLR output on both `axis=0` and `axis=1` is finite, non-negative, and preserves sparsity as expected for the seurat flavor.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf925bc0ae97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.