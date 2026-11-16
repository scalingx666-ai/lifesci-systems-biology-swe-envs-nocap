# Issue

**Title:** Generate test loom data with Hypothesis

## Description

Fix related bugs in API and especially implementation of
search_space::add_markers where element_type == "marker_gene": do not
assume that clustering ids are indexes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fac243958d1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.