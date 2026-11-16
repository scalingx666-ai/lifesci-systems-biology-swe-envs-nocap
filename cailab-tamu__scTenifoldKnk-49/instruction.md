# Issue

**Title:** Add GitHub Actions CI and release workflows

## Description

## Summary
- **CI** (`.github/workflows/R-CMD-check.yaml`): R CMD check on pushes to the default branch, pull requests and manual dispatch. Matrix: macOS, Windows and Ubuntu on R release, plus Ubuntu on R-devel and oldrel-1.
- **CD** (`.github/workflows/release.yaml`): on a version tag (`v*` or a tag starting with a digit), builds the source tarball, runs `R CMD check --as-cran` on it and attaches it to a GitHub release.
- Adds `^\.github$` to `.Rbuildignore` and an R-CMD-check badge to the README.
- scTenifoldKnk requires scTenifoldNet (>= 1.4.3), but CRAN only has 1.4, so the workflows install scTenifoldNet from GitHub (`github::cailab-tamu/scTenifoldNet`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e46221bc988b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.