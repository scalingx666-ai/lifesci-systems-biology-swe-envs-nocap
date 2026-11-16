# Issue

**Title:** v0.6.3

## Description

## v0.6.3

### Bug Fixes

#### `InvalidIndexError` when gene names are not unique (`sccellfie.preprocessing.prepare_inputs`)
- `preprocess_inputs` crashed with
  `InvalidIndexError: Reindexing only valid with uniquely valued Index objects`
  when slicing the AnnData by gene name (`adata2 = adata2[:, valid_genes]`).
  This aborted `run_sccellfie_pipeline` at the "Preparing inputs" step.
- Root cause: the function overwrites `adata.var_names` with the **corrected**
  gene names from `CORRECT_GENES` before filtering, and that index is not
  guaranteed to be unique. Duplicates arise in two ways:
  1. The input `adata.var_names` already contained duplicated symbols
     (`var_names_make_unique()` never run — common for symbol-indexed
     references or concatenated objects).
  2. A correction collapsed two distinct genes into the same symbol, e.g. a
     dataset carrying both `ADSS` and `ADSS2`, `G6PC` and `G6PC1`, `MT-CO1` and
     `COX1`, or `Gars1` and `Gars` in mouse. This case could **not** be fixed
     upstream by the user, since the collision is created by the correction
     itself.
- `preprocess_inputs` now drops duplicated gene names (keeping the first
  occurrence) right after applying the corrections, mirroring the behavior
  already present in `transform_adata_gene_names` for the Ensembl→symbol path.
  The number of dropped genes is reported when `verbose=True`.
- The same guard was added to the per-group branch of
  `sccellfie.sccellfie_pipeline.process_chunk` (`process_by_group=True`), which
  applies the same corrections and then slices by `met_genes`, and so could
  fail identically on any group after the first.

### Details

#### Preprocessing
- All masking in the affected block is now **positional (boolean)** rather than
  name-based, because `adata.var_names` itself may be non-unique — a name-based
  mask would fail in the same way as the original slice.
- Deduplication happens **after** the `CORRECT_GENES` mapping and is restricted
  to genes that survive the GPR-based gene filter, so no informative gene is
  removed by the guard alone.
- Users no longer need to call `adata.var_names_make_unique()` before running
  the pipeline, although doing so remains good practice, since it lets the user
  control which copy of a duplicated gene is kept.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bad8ea9afcd8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.