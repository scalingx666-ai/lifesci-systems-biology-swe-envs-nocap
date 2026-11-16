# Issue

**Title:** feat(skill_lint): require Skip when/if/for clause in v2 descriptions (PR-eval of skill rework)

## Description

## Summary

PR-eval (the first of 8 PRs in the Skill v2 rework continuation). Codifies
the routing-trigger half of the description contract that PR #1-#4 adopted
by convention: every v2 SKILL.md `description` must contain a `Skip when` /
`Skip if` / `Skip for` clause that names which neighbour skill the agent
should bounce to.

Without this clause, "Load when …" alone is half a routing trigger — the
agent learns when to load but not when to defer. PR #4 reviewer flagged
several near-collisions (sc-de vs bulkrna-de vs spatial-de) that the
`Skip when …` clause exists to prevent. This lint gates the next 74
migrations from drifting back into summary-style descriptions.

## What changed

- `scripts/skill_lint.py:67-89` — extended `_check_description` to require
  one of `("skip when", "skip if", "skip for")` after whitespace
  normalisation. The normalisation step matters because YAML folded
  (`>-`) / literal (`|`) scalars — used by 14 of 16 existing v2
  descriptions — can wrap "Skip when" across lines or introduce double
  spaces / tabs that bare substring matching would miss.
- `tests/test_skill_lint.py` — 4 new tests: 1 negative (no Skip clause),
  1 parametrised positive (each of the 3 variants), 1 parametrised
  whitespace-robustness fixture (newline / double-space / tab), 1 negative
  for "Skip otherwise" (bare Skip without connective → rejected).

## Backward compatibility

All 15 already-migrated v2 skills (bulkrna 13 + sc-de + spatial-de)
already follow the convention; `python scripts/skill_lint.py --all`
returns 90 ok / 0 fail unchanged. No retroactive description changes.

## Quality gate

One round of independent code-reviewer-agent review. Round 1 caught the
YAML folded-scalar whitespace risk (Important) which would have silently
let descriptions like `"Skip\nwhen"` slip through; the `.split()/join()`
normalisation in `scripts/skill_lint.py:75` is the round-1 fix.
No Critical findings.

## Test plan

- [x] `pytest tests/test_skill_lint.py` → 20 passed (was 16; +4 new)
- [x] broad sweep across 10 framework test files → 124 passed (was 120; +4 new)
- [x] `python scripts/skill_lint.py --all` → 90 ok / 0 fail
- [x] commit message + PR body verified Claude-trailer-free

## Diff scope

2 files changed, +83/-2 — purely the lint rule + its tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5cf97d730a83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.