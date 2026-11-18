# Issue

**Title:** bugfix: Update metaGEM.sh

## Description

Fix path to `config.yaml` file for `metaGEM.sh` script. 

As mentioned in #150, the `metaGEM.sh` wrapper cannot find the config file in question, a bug that was introduced after restructuring the repo to be compliant with the snakemake workflow catalogue [rules](https://snakemake.github.io/snakemake-workflow-catalog/?rules=true).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `978ae33afb71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.