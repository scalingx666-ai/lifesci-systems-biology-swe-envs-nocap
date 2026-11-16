# Issue

**Title:** Bugfix/302 increase grpc message size limits

## Description

This removes the limit on GRPC messages.

A fresh install might be needed, or the node_modules and package_lock.json files might need to be deleted from both the root directory AND the bindserver directory.

@dweemx Can you test with some larger loom files? My testing with a hacked GServer worked, but would be good to test on something real.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fdf94001be0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.