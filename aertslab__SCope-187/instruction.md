# Issue

**Title:** add singularity recipe, based on @tverbeiren's dockerfile

## Description

The singularity container is based on @tverbeiren's dockerfile at #186.

Usage:
```bash
sudo singularity build scope.simg Singularity
singularity run --app backend scope.simg
singularity run --app frontend scope.simg
```

Browse http://0.0.0.0:55850

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ca4edab2041`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.