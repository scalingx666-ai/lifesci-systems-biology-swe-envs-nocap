# Issue

**Title:** gs_heatmap: handled case 1 or less genes are to be plotted in the heatmap

## Description

in case there is only one gene to be plotted in the heat map, before a cryptic error was thrown, now a specific error indicating the problem is thrown. I added a test for it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fb79766f39b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.