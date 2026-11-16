# Issue

**Title:** Change the default settings in the TF-gene correlation calculation to include all cells (no dropout masking)

## Description

In the `modules_from_adjacencies` function, the default value of `rho_mask_dropouts` is changed to `False`. This now matches the behavior of the R version of SCENIC. Since this is likely to change the final output regulons slightly, warnings have been added to the logging system. The cli version has an additional option to turn dropout masking back on (`--mask_dropouts`).

The actual changes to the pySCENIC output are in the composition of the target genes in regulons. These are minor: in some cases the sign of the correlation switched depending on whether dropouts were masked, leading that target gene to be dropped or included in the module during pruning. In testing, this correlation switching occurred in a small minority of TF-gene interactions (6%).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8f3d9a6eee4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.