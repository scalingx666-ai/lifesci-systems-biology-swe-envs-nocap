# Issue

**Title:** Fix interestingness usage

## Description

The `interestingness` parameter was being used only to initialize the first `next_node` and nowhere else.  Also, the way it was used was flawed since it was picking the first key of the dictionary, which is not guaranteed to be the one with the highest interest.
    
This commit properly uses `interestingness` both for choosing the first node and to pick the best candidate for `next_node`, when more than on is available.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79da3806134e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.