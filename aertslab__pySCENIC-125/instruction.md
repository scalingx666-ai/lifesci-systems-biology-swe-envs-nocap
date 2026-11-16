# Issue

**Title:** Add properties for tracking regulons over multiple runs

## Description

In cases where we run pySCENIC multiple times, we want to track some additional parameters in the regulons object. These would be part of the final consolidated loom file for display on SCope. This is primarily:
* `gene2occurrence`: how often a target gene appears within a regulon

Full credit to @dweemx for these changes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef162504c021`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.