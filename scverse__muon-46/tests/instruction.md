# Issue

**Title:** Update tools.py

## Description

We should add a fragments file even if pysam is not installed. Otherwhise this can be confusing for the user if locate_fragments is called by load.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4f6e4453d72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.