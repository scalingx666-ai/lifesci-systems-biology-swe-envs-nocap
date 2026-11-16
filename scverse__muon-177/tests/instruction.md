# Issue

**Title:** Fix formatting, typo in mofa docs

## Description

In the mofa docstring `gpu_device` was a duplicate of `gpu_mode`. 
Also the description of `expectations` wrapped to an unindented line causing wrong formatting of the docs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c77d380e4bac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.