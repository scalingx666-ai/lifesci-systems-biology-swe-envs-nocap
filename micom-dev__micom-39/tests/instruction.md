# Issue

**Title:** Fix #37 by allowing the user to define the compression...

## Description

…type and level when building a zipped database. Default behavior stays the same (ZIP_STORED with no compression).

This commit reworks the behavior of the `compress` parameter and adds the optional parameter `compresslevel` to `micom.workflows.build_database()`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5101fed4accd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.