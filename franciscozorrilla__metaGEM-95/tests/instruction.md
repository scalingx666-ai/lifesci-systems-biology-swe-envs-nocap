# Issue

**Title:** Fix an error in kallisto2concut

## Description

The bash code of rule kallisto2concut was missing a directory '/'

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9796e3ab98e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.