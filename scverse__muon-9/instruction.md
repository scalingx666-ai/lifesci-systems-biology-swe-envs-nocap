# Issue

**Title:** Implement DSB normalization for CiteSEQ data

## Description

This introduces an optional dependency on scikit-learn. Results without denoising are identical to the R package. Due to random initialization and different implementations of the Gaussian mixture model, results with denoising are qualitatively similar, but not identical to results from the R package.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `92bd0287614f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.