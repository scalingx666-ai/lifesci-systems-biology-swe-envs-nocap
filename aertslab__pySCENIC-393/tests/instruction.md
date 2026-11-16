# Issue

**Title:** Pass max_similarity_fdr and min_orthologous_identity

## Description

Hi!

I have noticed that `max_similarity_fdr` and `min_orthologous_identity` were never passed to the functions when using the CLI code. Here is the small fix for that.

C

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29cb16079d86`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.