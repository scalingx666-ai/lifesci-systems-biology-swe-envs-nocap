# Issue

**Title:** Enable OSQP support

## Description

This is an experimental branch that enables native OSQP support and does not require a commercial solver.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `05dd2d349480`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.