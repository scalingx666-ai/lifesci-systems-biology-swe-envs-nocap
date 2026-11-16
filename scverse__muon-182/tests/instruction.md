# Issue

**Title:** Fix add_peak_annotation crash on empty distance values

## Description

## Description

Fix `add_peak_annotation` crashing when the peak annotation TSV contains empty distance values (intergenic peaks).

**Root cause:** When the distance column contains a mix of numeric values and empty strings, `pd.read_csv` infers it as `float64`. The existing code then tries to assign `""` into a numeric column, triggering `LossySetitemError`. On newer pandas with `StringDtype`, a similar issue occurs with `pd.NA` values.

**Fix:**
- Convert distance column to string via `astype(object).fillna("").astype(str)` to safely handle both numeric and nullable string dtypes
- Replace the multi-step `""` → `0` → `float` → `int` conversion with `pd.to_numeric(errors="coerce").fillna(0).astype(int)`, which handles all edge cases in one expression

## How has this been tested?

- Added regression test with exact data from the bug report (intergenic peaks with empty distance)
- Added test for semicolon-separated multi-gene annotations
- Existing tests pass (`pytest tests/` — 13 passed)

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `889d1ba05a8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.