# Issue

**Title:** Bugfix/403 motif only regulons

## Description

Distinguish between legacy formatted looms with only `Regulons`/`RegulonsAUC` vs newer looms with `MotifRegulons`/`MotifRegulonsAUC` and/or `TrackRegulons`/`TrackRegulonsAUC`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `020d665c5914`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.