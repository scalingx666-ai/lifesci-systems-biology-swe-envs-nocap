# Issue

**Title:** implement obsp/varp for MuData objects

## Description

Very basic implementation, but everything seems to work. Following AnnData, obsp/varp are always in-memory, even if the MuData object is file backed. We might want to change that in the future.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88608734c990`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.