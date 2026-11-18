# Issue

**Title:** Fix assembly stat

## Description

Assembly stats runs 'wc -l' on _compressed_ fasta output. It should be _decompressed_ prior to counting lines

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9796e3ab98e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.