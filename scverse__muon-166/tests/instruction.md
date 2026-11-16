# Issue

**Title:** make random state argument handling more consistent

## Description

- always default to non-None random_state (consistent within muon and with scanpy)
- fix condition before setting random state in .tl.leiden (, , )

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76ee5411b8a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.