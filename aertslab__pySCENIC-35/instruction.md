# Issue

**Title:** Add container support

## Description

I've added container recipes for both Docker and Singularity, and examples for running the containers. The containers essentially just provide a wrapper around the pySCENIC command line interface.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26db2c896503`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.