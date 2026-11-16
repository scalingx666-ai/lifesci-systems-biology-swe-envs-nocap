# Issue

**Title:** Switch build system over to flit

## Description

This follows up on the discussion in #25. I chose flit because it's more lightweight than poetry. Flit focuses on building and installing a package, whereas poetry tries to provide a full-fledged virtual environment manager. Also, Scanpy and Anndata use flit.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3744448fde50`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.