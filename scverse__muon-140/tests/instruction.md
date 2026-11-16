# Issue

**Title:** fixed reference to chromsome column in count_fragments_features

## Description

Fixing a reference where the column "Chromosome" was being called from the features dataframe despite "chr" and "chrom" being valid inputs as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eee8df0a28b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.