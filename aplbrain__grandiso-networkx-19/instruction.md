# Issue

**Title:** Memoize nodematch function calls

## Description

This adds a LRU-cache to the node match function calls, which greatly reduces the worst-case performance of subgraph search.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c6fc0dc4f10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.