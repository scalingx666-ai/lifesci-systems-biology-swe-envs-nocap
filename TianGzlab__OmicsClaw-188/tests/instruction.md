# Issue

**Title:** refactor(resolver): single-pass iter + tighten should_search_web default (OMI-12 audit P1 #1+#3)

## Description

## Summary
Two related routing-layer cleanups from the OMI-12 audit, bundled because the second one's snapshot diff is easier to read against the first one's refactor:

### 🟡 P1 #1 — Single iter over skills

Pre-refactor `resolve_capability` walked `iter_primary_skills` twice every chat turn:

1. `_detect_domain` iterated all 89 skills with the `_DOMAIN_SCORE_*` weights.
2. `resolve_capability` then iterated the same skills again with the `_SCORE_*` weights to populate candidates.

Both reads touched the same SKILL.md fields (alias, legacy aliases, description tokens, trigger keywords). The duplicate work is now folded into a single helper, `_score_skills_and_detect_domain`, which:

- accumulates both score sets in one pass,
- scans each skill's `trigger_keywords` exactly once and feeds both sides (candidate limit 3 / domain limit 2),
- returns `(detected_domain, candidates)`.

`resolve_capability` filters the precomputed candidate list to the detected domain instead of re-walking the registry. `_detect_domain` survives as a thin wrapper for external callers that only need domain detection.

### Correctness fix surfaced by the refactor

The earlier `_collect_query_keyword_matches` helper called `registry.build_keyword_map(domain=...)` and inherited its **last-write-wins** semantics for shared keywords. When both scoring sides share a walk we'd have to call `build_keyword_map(domain=None)`, which silently dropped scores: a keyword shared by `bulkrna-de` and any later-inserted skill would only ever score for the later skill. The "Run differential expression on bulk RNA-seq counts with DESeq2" query lost ~3.8 points on `bulkrna-de` under that path (7.88 → 4.05 in an interim regen).

**Fix**: iterate each skill's own `trigger_keywords` directly inside the shared walk and reuse the match list on both sides. `_collect_query_keyword_matches` is now unreferenced and deleted.

### 🟡 P1 #3 — `should_search_web` default

`should_search_web=True` used to be hard-coded on every `no_skill` outcome, defaulting the bot's LLM tool-use loop into a web-search step even for an ordinary omics query that just didn't happen to match a skill.

**Fix**: in the `no_skill` fallback, set `should_search_web = web_requested` (i.e. only when `_WEB_HINTS` matched the query). The explicit `_requests_new_literature_implementation` branch keeps its `True` because that path explicitly asked for external literature.

### Golden snapshot regen
- `should_search_web: true → false` for the "Detect doublets in my single-cell data using scDblFinder" query (no web hints) — exactly the intended behavioural change.
- Top-3 candidate orderings for tied-score cases refreshed to alphabetical (the snapshot was stale from before PR #187's tie-break — the test never asserted on top-3 ordering so the stale data went unnoticed).

The single `chosen_skill` / `coverage` / `domain` / `should_search_web` / `should_create_skill` line that the test actually checks remains stable for every other query.

### 4 new regression tests
- `test_resolve_capability_no_skill_fallback_defaults_should_search_web_to_false`
- `test_resolve_capability_no_skill_with_web_hints_still_searches_web`
- `test_resolve_capability_literature_implementation_still_searches_web`
- `test_score_skills_and_detect_domain_visits_each_skill_once` — monkey-patches `iter_primary_skills` to count calls per turn; asserts exactly one call.

## Test plan
- [x] `pytest tests/test_capability_resolver*.py tests/test_routing*.py tests/test_auto_routing_disambiguation.py tests/test_bot_n_epochs_routing.py` — **52 passed, 1 skipped, 5 xfailed** (4 new tests pass).
- [x] `pytest tests/test_capability_resolver*.py tests/test_routing*.py tests/test_skill_runner_contract.py tests/test_runtime_*.py tests/test_registry.py tests/test_execution_*.py tests/test_bot_n_epochs_routing.py` — 118 passed, 4 skipped, 5 xfailed; 1 pre-existing env failure unrelated (`fastapi` missing).
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_bot_runner_contract.py tests/test_interactive_omicsclaw_actions.py` — 104 passed; same 4 pre-existing failures as `main`.
- [x] `python omicsclaw.py list` — 89 skills × 8 domains.

## Out of scope (remaining P1 backlog)
- **#2** Drop the `-9 → 0` SIGKILL heuristic in favour of skills writing `result.json.status` (half-day + 89-skill coordination).
- **#4** Converge `SkillRunnerExecutor` onto `SubprocessExecutor` (~1 day).

Both deserve their own PRs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Refined fallback behavior when no matching capability is found—web search is now disabled by default and only enabled for explicit requests or literature-based implementation tasks.

* **Tests**
  * Added regression tests for capability resolution and skill scoring logic.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/188)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5921dd5ec920`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.