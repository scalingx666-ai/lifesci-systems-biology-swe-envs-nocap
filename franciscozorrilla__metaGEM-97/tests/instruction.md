# Issue

**Title:** Suggestion: Remove temporary output of CrossMapParallel

## Description

CrossMapParallel creates a lot of data on the scratch drive without ever removing - or needing - it. For only 81 samples, it caused over 30TB temporal garbage.
Instead, after successful completion of the rule, the temp directories should be removed from scratch folder.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9796e3ab98e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.