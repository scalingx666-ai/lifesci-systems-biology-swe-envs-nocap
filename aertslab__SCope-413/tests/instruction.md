# Issue

**Title:** Fix escaping regulon type determination logic early

## Description

Fixes bug where regulon AUC values wouldn't display for tracks or legacy regulon types

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a676c8c362ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.