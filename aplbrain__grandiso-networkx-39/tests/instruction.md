# Issue

**Title:** Add streaming match generation

## Description

This PR proposes "streaming match generation" for `grandiso`.

When working with large graphs and broad queries, the project currently has a number of places where results are queued up in lists. This requires having the full list at each step before proceeding to the next step. On top of that, if a `LIMIT` clause is specified, in some cases a large list needs to be built before the LIMIT clause is recognized and execution can be terminated.

This PR is as minimally invasive to the current code as possible. In most cases, the iteration logic is replaced with an inner function that runs a generator. When these generators are chained together, it effectively walks through the graph iteratively and enables returning results in a "streaming" fashion. 

There will be a corresponding PR in the GrandCypher project that will have a couple examples illustrating the full change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ff35624bdf6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.