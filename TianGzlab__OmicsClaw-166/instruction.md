# Issue

**Title:** feat(scaffolder): emit v2 layout (SKILL.md + parameters.yaml + references/) (PR-eval-3a)

## Description

## Summary

PR-eval-3a of the OmicsClaw "Skill v2" rework.  PR #164 (templates consolidation, merged) shipped the canonical v2 scaffold at `templates/skill/`.  Its reviewer flagged that the programmatic scaffolder at `omicsclaw/core/skill_scaffolder.py` was still emitting **legacy v1-shaped** skills (frontmatter with `metadata.omicsclaw` block; no `parameters.yaml` sidecar; no `references/*.md`) — so any freshly-scaffolded skill failed `scripts/skill_lint.py` immediately.

This PR rewrites the scaffolder to emit the canonical v2 layout and adds a unit-test guard so future regressions are caught at PR time rather than after merge.

### What changed

| Area | Change |
|---|---|
| `omicsclaw/core/skill_scaffolder.py` | `render_skill_markdown` → v2 frontmatter + 6 lint-required sections.  New `render_parameters_yaml` emits the 8-key sidecar.  New reference-template constants seed methodology / output_contract / r_visualization.  `references/parameters.md` is auto-generated via the shared renderer so it stays byte-for-byte aligned with the lint's freshness check.  `create_skill_scaffold` now writes all 7 v2 files per scaffold. |
| `omicsclaw/core/parameters_md.py` (new) | Canonical `render_parameters_md` used by both `scripts/skill_lint.py` and the scaffolder.  Replaces a sys.path-mutating lazy import. |
| `scripts/generate_parameters_md.py` | Slimmed to re-export from the package. |
| `scripts/skill_lint.py` | Imports `render_parameters_md` from the package; drops the `sys.path.insert(0, …/scripts)` line. |
| `omicsclaw/runtime/bot_tools.py:818-825` | `create_omics_skill` description now honestly claims v2 emission (reverts PR #164's "currently emits v1" disclaimer). |
| `skills/orchestrator/omics-skill-builder/omics_skill_builder.py` | Fixes the pre-existing `args.domain or "spatial"` dead-code bug.  Default is now `None`; demo mode falls back to `"spatial"` (the demo is intentionally a spatial CellCharter example); non-demo mode requires `--domain` explicitly.  The demo no longer lands in the spurious `skills/orchestrator/spatial-cellcharter-domains/` path. |
| `tests/test_skill_scaffolder.py` | Both `create_skill_scaffold` tests now assert all 5 v2 artifacts exist AND `lint_skill(skill_dir) == []`.  The pair only passes when both v2 shape and v2 content are correct. |

### Verification

```
$ python scripts/skill_lint.py --all 2>&1 | tail -1
ok   …/skills/spatial/spatial-velocity      (89 / 89 ok, 0 fail)

$ pytest tests/test_skill_scaffolder.py tests/test_skill_lint.py
        tests/test_metadata_roundtrip.py tests/test_lazy_metadata.py
        tests/test_lazy_metadata_sidecar.py tests/test_migrate_skill.py
        tests/test_skill_metadata_contract.py tests/test_registry_alias_contract.py
        tests/test_keyword_routing.py tests/test_registry_skills_snapshot.py
        tests/test_skill_runner_contract.py
230 passed   (1 deselected: pre-existing worktree-only failure)

$ python skills/orchestrator/omics-skill-builder/omics_skill_builder.py --demo --output /tmp/builder_smoke_v2
Created OmicsClaw skill scaffold at .../skills/spatial/spatial-cellcharter-domains
$ python scripts/skill_lint.py skills/spatial/spatial-cellcharter-domains
ok   skills/spatial/spatial-cellcharter-domains
```

### Reviewer findings amended into this commit

Independent `code-reviewer` agent: 0 Critical, 1 Important, 6 Suggestions.

| Severity | Finding | Resolution |
|---|---|---|
| Important | Test comment overclaimed what the lint assert catches (lint returns `[]` for any skill without `parameters.yaml`, so it would silently pass on legacy regression). | Rewrote the comment to credit the existence asserts as the real regression guard. |
| Suggestion | `sys.path` mutation from inside a runtime module. | Extracted `render_parameters_md` to `omicsclaw/core/parameters_md.py` so both the lint and the scaffolder import from the package; removed the mutation from both consumers. |
| Suggestion | Dead local `script_name` in `render_skill_markdown`. | Removed. |
| Suggestion | Duplicate `mkdir(references_dir)`. | Collapsed; promotion block reuses the dir created by v2 emission. |
| Suggestion | Precedence puzzle `(domain or source_bundle.domain if source_bundle else domain or "")`. | Rewrote as two readable lines. |

### Deferred to PR-eval-3b

PR #164's reviewer flagged 4 additional lint check classes that the existing lint can't detect (`BooleanOptionalAction` argparse companions, CSV column-name consistency, adata key consistency, path extension list extensions).  This PR keeps a narrow scope around the scaffolder emission rewrite; PR-eval-3b will add the new lint checks and the bulk-fix across the 89 existing skills.

## Test plan

- [x] `python scripts/skill_lint.py --all` clean (89/89 ok)
- [x] `pytest` core suite passes (230 passed)
- [x] End-to-end `omics-skill-builder --demo` emits a lint-clean v2 skill
- [x] Edge-case smoke (empty `methods` / `summary` / `request` / `trigger_keywords`) lints clean
- [x] Pre-existing worktree-only failures unchanged (`diff failures-before failures-after` empty)
- [x] No Claude attribution in commit or PR body

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e2dc3566d18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.