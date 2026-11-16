# Issue

**Title:** Don't set maxAge cookie on ping

## Description

Setting the cookie changes the page state and causes a re-render

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3bd635bc3a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.