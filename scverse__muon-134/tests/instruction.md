# Issue

**Title:** Fix #132

## Description

Hi!
I've encountered an issue when running `mu.pl.scatter` (#132) , as `sc.pl.scatter()` fails when passing the color as a list, as e.g. described in scverse/scanpy#1986
To avoid this issue, my suggested changes only take a string as input for the color instead of a string or a list.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7461aaa6bfd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.