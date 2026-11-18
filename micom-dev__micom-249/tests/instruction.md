# Issue

**Title:** Support .sbml model file extension

## Description

## Summary

I tested issue #131 against the current MICOM release (v0.39.1) and confirmed that `.sbml` files were still not supported by `micom.util.load_model()`.

Attempting to load a `.sbml` model resulted in:

`KeyError: '.sbml'`

This PR adds support for the `.sbml` extension and includes a regression test to ensure it can be loaded correctly.

## Changes

- Added `.sbml` to MICOM's model reader mapping.
- Added a regression test for `.sbml` model loading.

## Testing

- Reproduced the issue on MICOM v0.39.1 before the fix.
- `pytest tests/test_util.py::test_load_sbml_extension -q`
- `pytest tests/test_util.py -q`

Both tests pass after the fix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3bff1cacc745`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.