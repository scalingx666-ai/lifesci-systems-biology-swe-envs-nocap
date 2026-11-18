# Issue

**Title:** Remove profiling

## Description

This PR removes support for the `profiling` option, which added additional logic flow and was no longer needed. (If you still want to profile performance using a queue, you can use the `queues.ProfilingQueue` from the `queues` submodule.)

This is a breaking change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34ac616e2367`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.