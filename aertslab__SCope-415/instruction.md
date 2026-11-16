# Issue

**Title:** Search/Search space updates

## Description

Update terminal mappings for drosophila
    - Bump SS version as rebuild needed
Update order of search results
    - Correctly assign final categories to searches
    - Prefer genes/regulons over markers

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8af1e3dfc351`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.