# Issue

**Title:** Dramatically improve worst-case time

## Description

Some of the best characters-per-amount-of-improvement ratio I've ever written :)

In the worst-case of this algorithm (before), the worst-case is encountered when downstream nodes can't be filtered based upon connectivity to the partial candidate-mapping.

For example, in the star graph on 100 nodes, it takes us O(200) iterations to realize that we can't form any triangles: First to pick random nodes, and then to draw the first edge and realize there's nowhere for us to go.

This improvement checks the minimum degree of the receiving end of the edge, and short-circuits any search that is doomed to fail due to not-enough-places-to-go. In short, given a candidate mapping for any node, degree_motif ≥ degree_host.

---

The contrived worst-case star example is a new test in the GrandIso test-suite. Star(30K) takes nearly 30 seconds to run in the old model. In the new model, it is near-instantaneous.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b5db289c7b8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.