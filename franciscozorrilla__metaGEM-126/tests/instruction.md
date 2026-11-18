# Issue

**Title:** minor bugfix: maxbin Snakefile rule

## Description

maxbin was placing the resulting bins outside the expected folder, causing an error downstream during metaWRAP bin refinement. thanks to @LiZhihua1982 for reporting

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `245abb7faacb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.