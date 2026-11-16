# Issue

**Title:** CLR: add a flavor argument and add flavors stoeckius and standard

## Description

The Seurat implementation differs from both the standard definition of CLR and the version of CLR applied in the original CITE-Seq paper. Therefore, allow the user to choose the CLR flavor.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe40bd0f9688`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.