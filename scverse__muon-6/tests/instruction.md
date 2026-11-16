# Issue

**Title:** enable slicing for MuData objects

## Description

Unfortunately, the implementation is quite hacky, since I had to work around some peculiarities/hard-coded behavior of AnnData, but it seems to work for now. Briefly, tested, but there are probably still some bugs left

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eaacea3cc78c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.