# Issue

**Title:** plotting fixes

## Description

This PR attempts to make `.pl.scatter` and `pl.embedding` more predictable while simplifying our code and fixing some bugs.
- `use_raw` can no longer be `None`, it is either `True` or `False`. This is consistent with the scanpy API, leads to more predictable output, and allows us to considerably simplify our code.
- a new argument `gene_symbols` is supported, with the same functionality as in scanpy.
- the arguments `layer`, `use_raw`, and `gene_symbols` can be specified individually for each modality by passing dictionaries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dacf89910878`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.