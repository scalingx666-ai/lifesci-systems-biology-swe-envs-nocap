# Issue

**Title:** Build the client in production configuration in CI

## Description

This is to catch build failures in CI. This is prompted by several recent instances of build failures not being noticed in CI

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0d3352c1256`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.