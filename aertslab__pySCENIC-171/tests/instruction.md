# Issue

**Title:** CLI: Add gzip support for intermediate files

## Description

- Added methods to determine the file extension (which might contain a `.gz` ending)
- Reworked tests to determine which file import/export function to use
- Added optional gzip file connection to gene signatures
- Pandas read/write infers compression automatically from the file ending

Intermediate files are compressed based on the filename given in the command line arguments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3120aff123c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.