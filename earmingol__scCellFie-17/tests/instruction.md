# Issue

**Title:** Implemented memory efficient normalization

## Description

- Updated normalization function in [adata_utils.py](https://github.com/earmingol/scCellFie/blob/main/sccellfie/preprocessing/adata_utils.py) to be memory efficient.
- Added pertinent tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8dd0b489ecd7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.