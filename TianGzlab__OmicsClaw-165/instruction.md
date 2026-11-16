# Issue

**Title:** chore: stop tracking build/routing-baselines and ignore .claude/

## Description

## Summary
- Untrack `build/routing-baselines/*.json` (4 local benchmark artifacts) and remove the `!build/routing-baselines/` exception so they fall back under the existing `build/*` rule.
- Untrack `.claude/scheduled_tasks.lock` and add `.claude/` to `.gitignore` — Claude Code local state should not be committed.

## Why
These paths only hold per-machine state and benchmark scratch output. Tracking them creates noise in diffs and risks accidentally committing local settings.

## Test plan
- [x] `git ls-tree -r HEAD --name-only | grep -E "^(\.claude/|build/routing-baselines/)"` returns nothing on this branch.
- [x] `git check-ignore -v .claude/settings.local.json` and `... build/routing-baselines/before.json` both match the new rules.
- [x] No source code touched — pure repo hygiene.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9de986f5b8bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.