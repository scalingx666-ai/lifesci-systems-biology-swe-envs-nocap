# Issue

**Title:** Add option to save partial results

## Description

Added the argument `save_partial=False` which allows to save the results of the individual analyses before the final menr.
Useful to add new settings later on (or that the analysis crashes, which is the issue that I am having right now :P )

Feel free to decide whether to add it to the main branch or not...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `771fd654f4a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.