# Issue

**Title:** Fix non collapsed descriptions

## Description

This fixes the issue with duplicated search results, where descriptions are not collapsed

TODO:

- [x] Track down weird (extra) bug with double annotation results
  - Searching for a cluster annotation results in the annotation being doubled in the cluster description. Likely due to pdating the search space when adding a new annotation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa154376f268`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.