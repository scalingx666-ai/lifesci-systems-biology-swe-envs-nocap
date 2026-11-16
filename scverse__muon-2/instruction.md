# Issue

**Title:** File backing

## Description

first stab at file backed storage. Pretty hacky, but I couldn't find a cleaner way. Only tested with Visium data so far.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44c62226c950`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.