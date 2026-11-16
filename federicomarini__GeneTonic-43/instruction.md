# Issue

**Title:** Better colors

## Description

* `map2color()` has a behavior that better accounts for asymmetric ranges of values. This propagates to some of the functions that use it for mapping to colors, such as `enrichment_map()`, or `ggs_backbone()`.
* Some additional checks are in place for controlling the cases where the `z_score` of a geneset is detected as NA (e.g. because there was a mismatch between gene names and identifiers in the annotation).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9096e078090`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.