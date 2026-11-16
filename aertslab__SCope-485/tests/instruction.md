# Issue

**Title:** Disable pylint W1203

## Description

https://pycodequ.al/docs/pylint-messages/w1203-logging-fstring-interpolation.html
PyLint warns about not using lazy formatting for logging because
formatting messages that aren't printed is wasteful. This is
not interesting for our purposes and makes pylint output more
noisy than necessary.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `232e0762b690`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.