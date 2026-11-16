# Issue

**Title:** feat(singlecell): migrate sc-de to v2 (PR #2 of skill rework)

## Description

## Summary

PR #2 of the Skill v2 rework, rebased onto `main` after PR #1 (#133) merged.  Migrates `skills/singlecell/scrna/sc-de` end-to-end as the second pilot — first migration with non-trivial `param_hints` (5 methods × `advanced_params` × mixed-type defaults).

(Originally opened as zhou-1314/OmicsClaw#7 against the fork's stack base; closed and reopened here after rebase onto TianGzlab/main.)

## Framework increments delivered alongside

1. **`db448c3`** — `_build_sidecar` copies all legacy `metadata.omicsclaw` keys verbatim then `setdefault`s runtime fields (preserves `homepage`, `os`, `install`, `requires.bins/env/config`).
2. **`1c70219`** — heading bucketer routes `## Output Contract` to `references/output_contract.md` and `## Safety And Guardrails` to methodology instead of dropping.
3. Regression tests pin both behaviours.

## Quality gate

Two independent code-reviewer-agent passes during fork-PR phase. First pass found 3 Critical + 3 Important issues, all in hand-curated Gotchas (claimed `result.json` keys that didn't exist) and the missing output_contract section. All addressed in `1bb2db5` (preserved at the new tip `6cf9094` after rebase).

## Test plan

- [x] `pytest tests/test_lazy_metadata*.py tests/test_metadata_roundtrip.py tests/test_skill_lint.py tests/test_migrate_skill.py tests/test_skill_metadata_contract.py tests/test_registry_*.py tests/test_keyword_routing.py tests/test_skill_runner_contract.py` — **99 passed** post-rebase
- [x] `python scripts/skill_lint.py --all` — **90 ok / 0 fail**
- [x] `LazySkillMetadata` real-skill roundtrip on sc-de: bit-identical pre/post

## Diff scope

`9 files changed, +782/-284` — purely the sc-de migration + framework increments.  Zero overlap with the unrelated PR #132/#134 (memory cleanup) that landed on main between PR #1 and this PR.

## Out of scope

- 86 remaining skills.  Next: PR #3 spatial-de (also stacked, will rebase after this lands).
- Routing eval suite (Phase 4 per the original plan).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ae3b56f971a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.