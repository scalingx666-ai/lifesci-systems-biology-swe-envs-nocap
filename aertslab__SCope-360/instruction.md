# Issue

**Title:** Remove reliance on file hashes

## Description

- Remove all hash code
- Add thread locking
- Add search space update code
- Various code cleanups

This is not a backwards breaking change, but could change workflows that people are used to. Loom files can now no longer be updated directly via the backend (adding a new file still works). Deleting looms will also cause problems if the search space is not also removed.

Old search spaces will not be automatically deleted, but won't be used either

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8acb444406e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.