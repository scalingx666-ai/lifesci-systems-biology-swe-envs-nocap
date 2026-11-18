# Issue

**Title:** Warn when sample alignment removes replicates

## Description

When sample identifiers do not match, `pathway_daa()` currently intersects the inputs with `verbose = FALSE`, so a group can lose a replicate without any diagnostic. The shared alignment helper now always warns about sample removal, reporting retained counts and unmatched IDs from both inputs. The retained samples and statistical calculations are unchanged.

Adds regression coverage for quiet alignment, one-sided mismatches, reordered inputs, and the public DAA path; updates affected validation tests to expect the warning. A further heatmap regression verifies that a sample with positive abundance in the full table is retained when all selected pathways are zero in that sample, preserving all 12 samples and three replicates per group. The existing main-branch heatmap implementation already supports these zero columns; this test protects that behavior.

The tutorial explains sample auditing and the distinction between LinDA reference contrasts, a joint Wald test, and heatmap z-scores.

Validation of the final file tree: the full local test suite passed 1,992 assertions with 0 failures/errors, 5 skips, and 2 warnings. The tutorial knits successfully. Separately reproduced silent sample loss and the zero-column heatmap error with the v2.5.16 source; validated the Discussion #208 four-group Wald workflow against the official upstream LinDA source and an independent covariance calculation on simulated data. A direct ggplot2 workaround retains the zero-only sample and matches the current heatmap's row Z-scores without changing the analysis inputs or P-values.

Related discussion: https://github.com/cafferychen777/ggpicrust2/discussions/208

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c488133eb60`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.