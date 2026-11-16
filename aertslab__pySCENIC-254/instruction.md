# Issue

**Title:** fixed weight assignment when computing leading edge

## Description

Weights of genes in final regulons didn't match the weights from the regression (adjacencies data frame). 

The problem is when we compute the leading edge, where genes are sorted by ranking for pruning. Then, when we assign them the weights back, weights are sorted by alphabetical order. This leads to a gene-weight mismatch. 

The **leading_edge function** in the _recovery.py_ file was modified, so the weights get also sorted by ranking and the weight assignment now is fixed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc5d4989ddf7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.