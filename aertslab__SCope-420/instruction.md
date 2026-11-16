# Issue

**Title:** Disable resize detection in App.jsx

## Description

This fixes using multi-loom viewing in the compare tab in new versions of chrome and firefox.

Not sure what caused the bug to appear, but the resize detector was being triggered resulting in a re-render and resetting the page when switching to multi-loom.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69a2bff27e84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.