# Issue

**Title:** Add grandiso.queues submodule

## Description

This PR adds a `grandiso.queues` submodule, which enables you to specify a queue class to use instead of the default simplequeue. 

This will ultimately enable memory-mapped queues, and currently enables a user to choose between breadth-first, depth-first, or memory-profiled queues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `570d1dd87f4c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.