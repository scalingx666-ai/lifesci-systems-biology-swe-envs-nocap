# Issue

**Title:** Add FastAPI HTTP interface

## Description

* Adds a top-level server entrypoint. Start with `poetry run hypercorn main:scope_api --reload`
* Adds hypercorn and FastAPI dependency

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e3c6e97bdb1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.