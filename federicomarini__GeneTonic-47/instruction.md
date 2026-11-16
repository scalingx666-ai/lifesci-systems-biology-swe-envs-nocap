# Issue

**Title:** Ridge genesets

## Description

This branch adds some functionality to the `enhance_table` function, in a way that the summaries can now be done also as ridge plots, colored optionally by the z_score of each geneset.

Looks like more or less like this

![image](https://user-images.githubusercontent.com/7447478/215512555-f0681335-6f09-436b-bf4b-bd2f82374386.png)

... so that the individual genes contributing to the density are still stylized visible below each profile.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c32b540efc7c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.