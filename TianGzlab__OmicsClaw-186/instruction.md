# Issue

**Title:** refactor(resolver): documented scoring weights + golden routing snapshot (OMI-12 P2.8+P2.9)

## Description

## Summary
OMI-12 P2.8 + P2.9 — same diff because they reinforce each other:

- **P2.8** lifts the resolver's scoring weights out of inline arithmetic into documented module-level constants and routes the trigger-keyword signal through `registry.build_keyword_map()` instead of rescanning each skill's `trigger_keywords` from inside the per-skill loop.
- **P2.9** pins the live `chosen_skill` / `coverage` / `domain` for 20 representative queries in `tests/fixtures/golden_routing/snapshot.json` so any future weight tweak that re-ranks even one query surfaces as a single, query-named test failure.

This is a pure refactor + new test PR. Behaviour is preserved byte-for-byte: same matcher (`_mentions_phrase`), same weights, same thresholds; only the spelling changes.

## What changes

### P2.8 — Documented weights

| Constant | Old magic number | What it controls |
|---|---|---|
| `_SCORE_ALIAS_MENTION` | `12.0` | User typed the canonical alias |
| `_SCORE_LEGACY_ALIAS_MENTION` | `9.0` | User typed a `SKILL.md legacy_aliases` entry |
| `_SCORE_DESCRIPTION_OVERLAP_PER_TOKEN` / `_CAP` | `0.85` / `8` | Query token ∩ description tokens |
| `_SCORE_TRIGGER_KEYWORD_MIN` / `_MAX` / `_LENGTH_DIVISOR` / `_LIMIT` | `1.5` / `4.5` / `6.0` / `3` | Length-weighted keyword match |
| `_SCORE_PARAM_HINT_MATCH` | `3.0` | Query method matches a param hint |
| `_DOMAIN_SCORE_FILE_PATH` / `_ALIAS_MENTION` / `_LEGACY_ALIAS_MENTION` / ... | `5.0` / `8.0` / `6.0` / ... | Domain detection signals |
| `_RESOLVE_NO_SKILL_THRESHOLD` | `3.0` | Below this top-1 score → `no_skill` |
| `_RESOLVE_CLOSE_SECOND_GAP` | `1.5` | Top-1 minus top-2 must exceed this for an `exact_skill` commit on composite queries |
| `_RESOLVE_CONFIDENCE_DIVISOR` | `14.0` | `top.score / divisor → confidence` |
| `_RESOLVE_NO_SKILL_CONFIDENCE_DIVISOR` / `_CAP` | `10.0` / `0.35` | Fallback confidence on the `no_skill` branch |

Trigger-keyword scoring now runs through a pre-computed `{alias: [matched_keywords]}` map built once per `resolve_capability` call via `registry.build_keyword_map()` — the same inverted index the registry was already maintaining. `_candidate_score` consumes that map instead of rescanning the skill's own `trigger_keywords`. `_mentions_phrase` (the actual matcher) and the per-keyword score formula are unchanged.

### P2.9 — Golden routing snapshot

| File | Purpose |
|---|---|
| `tests/fixtures/golden_routing/snapshot.json` | 20 queries × `{chosen_skill, coverage, domain, should_search_web, should_create_skill, top_3_candidates}` |
| `tests/test_capability_resolver_golden.py` | Parametrised pin test (one case per query), corpus-breadth sanity check, `regenerate()` helper for developer use |

The corpus covers every domain (spatial, single-cell, bulkrna, metabolomics, genomics, proteomics, literature) and every decision bucket (`exact_skill`, `partial_skill`, `no_skill`, `skill_creation`). It deliberately includes a few known misroutes that exist on `main` today (scRNA-seq preprocessing → `spatial-preprocess`, WGCNA → `bulkrna-ppi-network`, XCMS → `spatial-preprocess`) so a future fix that *improves* them surfaces in the diff — and so an unrelated tuning that accidentally regresses to the same bad outcome is unaffected.

## Test plan
- [x] `pytest tests/test_capability_resolver.py tests/test_routing_regression.py tests/test_auto_routing_disambiguation.py tests/test_capability_resolver_golden.py` — **42 passed, 1 skipped, 4 xfailed**; the same 2 pre-existing routing failures (WGCNA, XCMS) that exist on `main` reproduce here and are now also captured in the snapshot.
- [x] `pytest tests/test_capability_resolver*.py tests/test_routing*.py tests/test_skill_runner_contract.py tests/test_runtime_*.py tests/test_registry.py` — 93 passed, 3 skipped, 4 xfailed.
- [x] `python omicsclaw.py list` — 89 skills × 8 domains.

## Regenerating the snapshot
After an intentional weight change:
```bash
python -c "from tests.test_capability_resolver_golden import regenerate; regenerate()"
```
Then review the diff before committing.

## Remaining backlog (per OMI-12)
- **P3** — structured event logging, per-skill timeouts, unified subprocess strategy

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Tests**
  * Added golden routing snapshot test suite with parametrized tests covering multiple domains, including validation across exact_skill, partial_skill, and no_skill coverage buckets.

* **Refactor**
  * Refactored capability resolver with explicit configuration constants for weights and thresholds, plus optimized keyword matching precomputation.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/186)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6654a4e7989`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.