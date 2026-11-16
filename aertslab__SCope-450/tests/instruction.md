# Issue

**Title:** Update client deps to satisfy vulnerability checks

## Description

Update deps to silence several vulnerability errors. Also remove google protobuf and grpc deps that are not used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af04aa3390bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.