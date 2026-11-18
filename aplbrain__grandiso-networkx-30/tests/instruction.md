# Issue

**Title:** Python 3.6 support

## Description

`SimpleQueue` has been introduced in Python 3.7.
Not sure it's a goal of the project to support Python 3.6, but it seems like easy enough to achieve to be worth it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `322e9e223942`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.