# Issue

**Title:** Implement multimodal nearest neighbor search

## Description

Multimodal nearest neighbor search for two modalities was described in the Seurat 4 paper ([Hao et al, 2020](https://doi.org/10.1101/2020.10.12.335331)) and was extended to arbitrary modality numbers in the TEA-seq paper ([Swanson et al, 2020](https://doi.org/10.1101/2020.09.04.283887)).

This implementation should also be able to handle data sets with cells that were only observed in a subset of the modalities, but I couldn't test that. On CiteSEQ data, UMAP plots generated with this implementation look reasonable. This PR also adds a thin wrapper around SciPy's umap function to easily perform umap dimensionality reduction for the multimodal graphs.

Runtime and peak memory consumption are still a problem for large data sets. I did memory and runtime profiling, both are due to UMAP's nearest_neighbor search, so I'm not sure if I can do anything here.

This PR promotes sklearn to a hard dependency and adds umap-learn and numba as dependencies. All three are hard dependencies of scanpy, so no additional dependencies are introduced.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82b9992d62a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.