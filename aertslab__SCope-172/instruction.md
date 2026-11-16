# Issue

**Title:** Fix bug "Error: ENOENT: no such file or directory, scandir 'SCope/ass…

## Description

…ets'" when running "npm run dev" when installing SCope. Assets directory needs to exist.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3bca076b0f52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.