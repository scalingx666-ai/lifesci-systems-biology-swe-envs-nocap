# Issue

**Title:** Calculating correlation between gene-based regulon AUC and region-based regulon AUC

## Description

Hey, as suggested in #58 I had a go at drafting a function to calculate the correlation between gene-based AUC and region-based AUC! It was simpler than I expected :) 

I figured a pull request was the simplest way to share the code. This has only had very basic testing on the data I'm working with, nothing systematic yet. Feedback would be very welcome!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22735ca32370`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.