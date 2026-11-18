# Issue

**Title:** Permit falsy node IDs

## Description

Previously, falsy node IDs (e.g. `""`, `0`, `False`) were interpreted as a "null" node; in other words, edges to that node were ignored. This was helpful in cases where knowing the structure of the graph was useful but the edges that terminated in the null nodes weren't useful for identifying subgraph isomorphisms.

In order to bring this package more in line with the NetworkX API, this behavior is now no longer permitted, and all nodes are treated the same.

- [x] Tests
- [x] Implementation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18c703e7668a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.