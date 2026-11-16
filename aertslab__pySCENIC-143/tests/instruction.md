# Issue

**Title:** Ability to set a fixed seed for AUCell and regulon thresholds derivation

## Description

AUCell uses a random sampling of the expression matrix to break ties in the ranking step. The CLI parameter `--seed` or `aucell` function parameter `seed` uses a fixed seed for this step

The regulon thresholds also depend on random sampling in the binarization step (bimodality test: `np.random.uniform`), and the seed parameters apply here as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3764c41605a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.