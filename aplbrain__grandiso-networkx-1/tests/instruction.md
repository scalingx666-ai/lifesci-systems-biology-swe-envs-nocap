# Issue

**Title:** Add undirected-graph support

## Description

No API changes. 

You don't need to specify `directed=True`; if both motif and host are directed, it's set automatically. Otherwise, the question is ill-defined and an undirected mode is used instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7eeec8f96fec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.