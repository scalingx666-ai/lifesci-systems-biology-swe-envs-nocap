# Issue

**Title:** fix(resolver+bot): stable WGCNA tie-break + drop dead spatial-domain-identification branches (OMI-12 audit P0)

## Description

## Summary
Two real bugs from the OMI-12 post-P2.9 audit, each addressable in well under an hour:

### 🔴 P0 #1 — Golden routing test flapping on `main`

`tests/fixtures/golden_routing/snapshot.json` pins the WGCNA query to `bulkrna-coexpression`, but the live resolver returns `bulkrna-ppi-network` on a fresh checkout:

```
FAILED tests/test_capability_resolver_golden.py
chosen_skill drifted for 'Build a WGCNA co-expression network ...':
expected 'bulkrna-coexpression', got 'bulkrna-ppi-network'.
```

Root cause: **both skills score exactly 7.250**, and `candidates.sort(key=lambda c: c.score, reverse=True)` is Python-stable — the winner is whichever `registry.iter_primary_skills` yielded first, which depends on filesystem traversal at registry load. The PR #186 `regenerate()` happened to land on `bulkrna-coexpression`; subsequent checkouts on a different filesystem ordering land on `bulkrna-ppi-network`.

**Fix**: `candidates.sort(key=lambda c: (-c.score, c.skill))` — same primary key, deterministic alphabetical tie-break. `bulkrna-coexpression < bulkrna-ppi-network` so the snapshot matches under any iteration order.

**Side benefit**: `test_routing_regression.py::clear WGCNA on bulk` was one of two strict-fail tests on `main`; it now passes deterministically. The XCMS case was already moved to xfail upstream.

### 🔴 P0 #2 — Dead `spatial-domain-identification` branch in bot adapters

`bot/skill_orchestration.py:489` and `bot/tool_executors.py:286` both branched on `canonical_skill == "spatial-domain-identification"` to pick `--epochs` vs `--n-epochs`. But the registry's canonical alias for that skill is now `spatial-domains` — the rename happened in an earlier PR, so the `if` branch **never fires**. The bot always sent `--n-epochs`, and `argv_builder.filter_forwarded_args` quietly rewrote it to `--epochs` per the receiving skill's allow-list. Three implementations of the same rewrite, two of them dead.

**Fix**: collapse both bot branches to unconditional `["--n-epochs", str(n_epochs)]` and let `argv_builder` own the rewrite. Comments document why.

## New regression tests
- `tests/test_capability_resolver.py::test_resolve_capability_breaks_score_ties_alphabetically` — pins the WGCNA case to `bulkrna-coexpression` and asserts top-1/top-2 are alphabetically ordered when tied.
- `tests/test_bot_n_epochs_routing.py` (4 tests) — AST-greps both bot modules to ensure the dead conditional doesn't sneak back, sanity-checks the argv-builder rewrite the bot now depends on, and asserts the registry still resolves the legacy alias to `spatial-domains` (a future SKILL.md rename would have to revisit this PR).

## Test plan
- [x] `pytest tests/test_capability_resolver.py tests/test_capability_resolver_golden.py tests/test_routing_regression.py tests/test_auto_routing_disambiguation.py tests/test_bot_n_epochs_routing.py` — **48 passed**, 1 skipped, 5 xfailed (WGCNA strict-fail flipped to pass; everything else unchanged).
- [x] `pytest tests/test_capability_resolver*.py tests/test_routing*.py tests/test_skill_runner_contract.py tests/test_runtime_*.py tests/test_registry.py tests/test_execution_default_executor.py tests/test_execution_executors.py tests/test_bot_n_epochs_routing.py` — 114 passed, 4 skipped, 5 xfailed; 1 pre-existing env failure unrelated (`fastapi` missing).
- [x] `pytest tests/bot/test_skill_orchestration.py tests/test_metadata_roundtrip.py tests/test_bot_runner_contract.py tests/test_interactive_omicsclaw_actions.py` — 104 passed; same 4 pre-existing failures as `main` (pydantic version + bot logger-name assertion).
- [x] `python omicsclaw.py list` — 89 skills × 8 domains.

## Out of scope (P1 backlog from the audit)
- Share single iter over skills between `_detect_domain` and `resolve_capability` (O(2N) → O(N))
- Drop the `-9 → 0` SIGKILL heuristic in favour of skills writing `result.json.status`
- Default `should_search_web=False`, fire only on `_WEB_HINTS`
- Converge `SkillRunnerExecutor` onto `SubprocessExecutor`

These need their own PRs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfc30352894f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.