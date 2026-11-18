# Issue

**Title:** Update pathway_errorbar.R - applying left join to properly map groups to samples

## Description

A proper mapping from sample names to their corresponding groups is achieved by applying a left_join function. This requires declaring additional parameters in the pathway_errorbar function, which are: 

df_meta: The metadata data frame
meta_id_col: This is the key column for matching the abundance data with the grouping variable in the metadata. 

Function parameters df_data and meta_group_col are redundant with Group and abundance, but are useful to separate the mapping code, which starts at line 286.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `353181da9bb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.