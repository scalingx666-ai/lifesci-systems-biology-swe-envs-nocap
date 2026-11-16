# Issue

**Title:** Fix `tfidf` using the wrong layer

## Description

TF-IDF seems to be using `adata.X` for some of its computations even when `from_layer` is defined.

This leads to the following error when `.X` is not defined.

Input:

    AnnData object with n_obs × n_vars = 600 × 1500
        obs: 'tech', 'celltype', 'size_factors', 'n_counts', 'cell_type', 'batch'
        var: 'n_cells', 'feature_name'
        uns: '_from_cache', 'data_reference', 'data_url', 'dataset_description', 'dataset_id', 'dataset_name', 'dataset_organism', 'dataset_reference', 'dataset_summary', 'dataset_url', 'var_names_all'
        layers: 'counts'

Code:

```python
normalized_counts = ac.pp.tfidf(
  adata,
  from_layer="counts",
  to_layer="tfidf"
)
```

Error:

    Traceback (most recent call last):
      File "/tmp/viash-run-atac_tfidf-6y8F0o.py", line 39, in <module>
        normalized_counts = ac.pp.tfidf(
                            ^^^^^^^^^^^^
      File "/usr/local/lib/python3.11/site-packages/muon/_atac/preproc.py", line 106, in tfidf
        idf = np.asarray(adata.shape[0] / adata.X.sum(axis=0)).reshape(-1)
                                          ^^^^^^^^^^^
    AttributeError: 'NoneType' object has no attribute 'sum'

Not only that, but it could mean that muon is accidentally computing incorrect results when `.X` and `from_layer` is used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94917d23291f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.