# Issue

**Title:** Reorganise and abstract SCope server config

## Description

* Creates an "outer layer" config that the "inner layer" business code can depend on.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cda1ed861748`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.