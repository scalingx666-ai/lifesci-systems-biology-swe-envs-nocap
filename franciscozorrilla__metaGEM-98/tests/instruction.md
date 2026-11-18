# Issue

**Title:** Fix an issue with metabat2

## Description

In combination with the CrossMapParallel workflow, the 'rule metabat' has to be used (instead of metabatCross).
This rule failed due to a 'too many positional arguments' error in metabat2.
The current interfact of metabat2 _does not_ support to directly supply mapping files.
Instead, the mapping file is first converted to a depth file, the latter is used then directly with metabat2.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9796e3ab98e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.