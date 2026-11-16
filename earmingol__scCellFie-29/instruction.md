# Issue

**Title:** v0.6.1

## Description

## v0.6.1

### New Features

#### Memory-efficient `agg_expression_cells` (`sccellfie.expression.aggregation`)
- `agg_expression_cells` was rewritten to bound peak memory on large (single-cell
  and spatial) datasets. Genes are now subset **before** any densification, so a
  sparse column slice stays sparse and only the requested columns are ever
  materialized; groups are aggregated one at a time instead of densifying the
  whole matrix.
- New **sparse fast paths** compute the common reductions without densifying at
  all:
  - `mean` (with implicit zeros) → sparse column mean.
  - `mean` with `exclude_zeros=True` → `column_sum / column_nnz`.
  - `fraction_above` with `threshold >= 0` → counts stored non-zeros directly
    (only non-zeros can exceed a non-negative threshold).
- `top_mean` is now **vectorized** with `np.partition` instead of
  `np.apply_along_axis`, which is substantially faster on wide matrices while
  preserving the exact NaN-handling and top-`percent` semantics.

#### `chunk_size` for exact, memory-bounded percentile aggregations
- `agg_expression_cells(..., chunk_size=N)` densifies at most `N` **genes** at a
  time for the aggregations that require a dense block (`median`, `25p`, `75p`,
  `trimean`, `topmean`, and any dense input). This is the memory relief for the
  percentile-based functions, which the sparse fast paths cannot cover.
- The chunking is over **genes, never cells**, so every cell of a group is still
  seen for each gene — results are **bit-identical** to the unchunked path
  (percentiles/order-statistics stay exact). `chunk_size=None` (default)
  aggregates each group in a single block, preserving existing behavior.
- Peak dense memory drops from `max_group_cells × n_genes` to
  `max_group_cells × chunk_size` (down to a single gene column at a time).

#### `dtype` cast for `agg_expression_cells`
- New `dtype=` argument (e.g. `np.float32`) casts dense group blocks before
  aggregation to further reduce memory. `None` (default) keeps the source dtype.

#### Fixed-number per-group subsampling (`sccellfie.preprocessing.fixed_number_subsample_adata`)
- `fixed_number_subsample_adata(adata, group_column, target_n=1000, random_state=0)`
  subsamples an AnnData to a **fixed number of cells per group**, a sibling to the
  existing fraction-based `stratified_subsample_adata`. Useful for balancing
  group sizes (e.g. capping each cell type at `N` cells) regardless of the
  original group proportions.
- Groups with fewer than `target_n` cells are kept in full and a `UserWarning`
  is issued naming the group and its size. Reproducible via `random_state`.

### Details

#### Aggregation
- `fraction_above` still raises a `ValueError` up front when no `threshold` is
  provided.
- `exclude_zeros` and the `dtype` cast are applied per gene-window block in the
  densifying path, so their extra copies are also bounded by `chunk_size`.
- `use_raw=True` correctly uses `adata.raw.var_names` (which may differ from
  `adata.var_names`) when subsetting genes.

### Usage Examples

#### Memory-bounded aggregation with exact percentiles
```python
import numpy as np
import sccellfie

# Sparse mean / fraction_above never densify — no tuning needed.
means = sccellfie.expression.agg_expression_cells(
    adata, groupby='cell_type', agg_func='mean',
)

# Percentile-based aggregations densify; bound peak memory by capping the number
# of genes materialized at once. Results are identical to chunk_size=None.
trimean = sccellfie.expression.agg_expression_cells(
    adata, groupby='cell_type', agg_func='trimean',
    chunk_size=500,        # densify at most 500 genes at a time
    dtype=np.float32,      # optional: halve the dense-block footprint
)
```

#### Fixed number of cells per group
```python
import sccellfie

# Cap every cell type at 1000 cells (groups with fewer are kept in full).
balanced = sccellfie.preprocessing.fixed_number_subsample_adata(
    adata, group_column='cell_type', target_n=1000, random_state=0,
)
balanced.obs['cell_type'].value_counts()   # each group <= 1000
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eea33820b3d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.