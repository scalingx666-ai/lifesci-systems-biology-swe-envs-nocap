# Issue

**Title:** Remove pyscenic dependency

## Description

This change removes the pyscenic dependency and the gene set enrichment code that depended on it. This allows us to use Python 3.9 and drop Python 3.7 support.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0d3352c1256`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.