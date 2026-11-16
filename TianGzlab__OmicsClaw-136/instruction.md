# Issue

**Title:** feat(spatial): migrate spatial-de to v2 (PR #3 of skill rework)

## Description

## Summary

PR #3 of the Skill v2 rework, rebased onto main after PR #2 (#135) merged.
Migrates `skills/spatial/spatial-de` — the heaviest legacy skill (476-line SKILL.md,
34 allowed_extra_flags, 3 methods × up to 16 params each).

(Originally opened as zhou-1314/OmicsClaw#8 against the fork's stack base;
closed and reopened here after rebase onto TianGzlab/main.)

## Framework increment

- `cedd468` — adds `'visualization contract'` to `OUTPUT_HEADINGS` so spatial
  skills' `## Visualization Contract` heading routes to `references/output_contract.md`.
  Regression test included. Zero collateral with bulkrna-de + sc-de (neither
  uses this heading).

## Quality gate

Two independent code-reviewer-agent passes during fork-PR phase. Round 1 found
3 Important issues in hand-curated Gotchas; all addressed in `296aa30`
(originally `6785a5c` pre-rebase).

## Test plan

- [x] `pytest tests/...` → 101 passed
- [x] `python scripts/skill_lint.py --all` → 90 ok / 0 fail
- [x] LazySkillMetadata real-skill roundtrip on spatial-de: bit-identical pre/post

## Diff scope

9 files changed, +960/-454 — purely the spatial-de migration + framework increment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f09e35fafc15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.