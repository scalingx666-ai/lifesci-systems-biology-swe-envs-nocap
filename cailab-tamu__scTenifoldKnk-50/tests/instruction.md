# Issue

**Title:** scTenifoldKnk 1.1.5: leave the knocked-out genes out of the dRegulation null

## Description

## Summary

- **`dRegulation()` gains `gKO`** and leaves the knocked-out genes out of the expectation of the chi-square test: FC = d^2 / mean(d^2 of the genes not in `gKO`). This is what the package did up to 1.0.3. Commit 1ab43d9 (released in CRAN 1.1 and 1.1.1-1.1.4) changed it to the mean over all genes. The knocked-out genes then dominate that mean, and often only they come out significant. This is why the Dmd result of the manuscript could not be reproduced (#45). `scTenifoldKnk()` passes `gKO`, and each target gene in transcriptome-wide mode. Distances, Z and the gene ranking do not change; FC, p-values and adjusted p-values do.
- **Only the WT network is returned** in `tensorNetworks` (#9). The KO network is WT with the `gKO` rows set to 0, and keeping both roughly doubled the size of the output. The docs show how to rebuild it.
- **Tests**: new `tests/testthat` for `dRegulation()` (single and multiple `gKO`, invalid input, `gKO = NULL`) and for single-gene, multi-gene and transcriptome-wide knockouts. The pipeline tests fail on 1.1.4 and pass here.
- **Manuscript reproduction** (`inst/manuscript/DMD/Code/reproduce_GSM4116571.py`, not part of the package build). It rebuilds the Dmd result from `Data/` with scTenifoldpy >= 0.5.1, and `DMD_DataProcessing.R` notes where its commented code differs from the run that produced `Results/`.

## Reproducing the published Dmd table

The April 2020 run used R < 3.6. Its `sample()` default ("Rounding") picked other cells than `set.seed(1)` picks now. It also used raw counts, `K = 5` rounded to 1 decimal, `d = 2`, and removed the ribosomal and mitochondrial genes after the alignment. With those conditions, the script gives:

- a WT network identical to `Results/GSM4116571.RData` in all 95.7M entries;
- the same 190 genes with p.adj < 0.05 as `scTenifoldKnk_SRS4245406.csv`, with the same top genes.

The fixed `dRegulation()` reproduces the published FC from the saved alignment to 5.5e-15. With the 1.1.4 behaviour, the same data give 1 significant gene.

On GSM4116571 with default settings, Dmd gives 56 significant genes, up from 2. Dmd + Utrn together give 57, with both knocked-out genes significant. The mean FC of the other genes is exactly 1 in both cases.

## Checks

- `R CMD check --no-manual`: Status OK
- testthat: 25 passed, 0 failed

scTenifoldpy gets the same fix, and its R-parity fixtures regenerated with this version, in a separate PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `868355fef815`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.