# Issue

**Title:** Fix motif annotation selection when using clustered motif dbs

## Description

When using the cluster database, it is possible to have a TF annotated to a cluster directly and indirectly (because we pull the annotations of all motifs in the cluster). This causes problems in the code when merging the annotation to the motif enrichment table in `module2features_auc1st_impl` as the same cluster can appear in more than a row in the annotation. This is a small fix in which we keep the direct annotation if available (so it will be part of direct regulons); if the cluster has only indirect annotations we take one (and will be part of extended regulons).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba06f54c1cf2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.