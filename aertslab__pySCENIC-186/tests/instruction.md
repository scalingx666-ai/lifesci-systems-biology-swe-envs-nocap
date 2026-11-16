# Issue

**Title:** Dev

## Description

* Fix bug in motif url construction (#158)
* Integrate arboreto multiprocessing script into pySCENIC CLI
* cisTarget step: Check for modules with zero db overlap and skip them (#158, #177, #132, #85)
* Bugfix in TF-gene correlation calculation. Quit with error if there is a mismatch between the genes present in the GRN and the expression matrix (#103, #149 
* Error message when regulons file is empty (#133)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c73e44b76282`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.