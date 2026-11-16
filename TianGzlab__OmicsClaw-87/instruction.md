# Issue

**Title:** feat(io): clear error messages for unsupported input formats

## Description

## Summary

- `smart_load` now catches `.rds`/`.robj`/`.rdata` (Seurat) and `.xlsx`/`.xls` (Excel) before attempting to read
- Raises `ValueError` with exact conversion commands instead of crashing with a cryptic traceback
- Unknown extensions still attempt h5ad read, but wrap failure with a user-friendly format list

## User-facing behavior

**Before:** User uploads `.rds` → `sc.read_h5ad()` → `HDF5ExtError: Unable to open file` (incomprehensible)

**After:**
```
Seurat/R object detected (.rds), OmicsClaw requires AnnData format.

Convert in R first:
  library(Seurat)
  library(SeuratDisk)
  obj <- readRDS("my_data.rds")
  SaveH5Seurat(obj, filename = "converted.h5seurat")
  Convert("converted.h5seurat", dest = "h5ad")

Then run:
  python omicsclaw.py run sc-standardize-input --input converted.h5ad --output <dir>
```

## Test plan

- [ ] `.rds` / `.robj` / `.rdata` → Seurat conversion instructions with SeuratDisk + sceasy
- [ ] `.xlsx` / `.xls` → pandas conversion instructions
- [ ] `.h5ad` / `.csv` / `.h5` / `.loom` → no change (still supported)
- [ ] Unknown extension → attempts h5ad, wraps failure with supported format list

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82e897846f78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.