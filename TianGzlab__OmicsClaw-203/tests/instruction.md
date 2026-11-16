# Issue

**Title:** fix(memory): expose remember tool on declarative preference statements

## Description

## Summary

Fixes a silent persistence-failure bug visible in the desktop app: when a user states a persistent preference declaratively ("以后请用中文回答", "from now on use DESeq2") **without** uttering a 记住/remember trigger word, the LLM was unable to persist it — the `remember` tool was filtered out of its tool list by the keyword-gated `memory_in_use` predicate. The LLM would reply with a verbal "got it" not backed by a DB write, and the next session lost the preference. The desktop "memory module" UI thus never showed the user's stated preference.

### Root cause

`omicsclaw/runtime/tool_predicates.py` mapped `remember` → `memory_in_use`, which fires only on `\b(remember|forget|recall|memorize)\b|记住|忘记|忘掉|回忆`. Declarative preferences without these keywords were silently dropped.

### Fix

Introduce a new `preference_statement_intent` predicate that catches declarative persistent-preference language in Chinese (`以后/今后/始终/一直/总是/每次` + preference verb, `默认 + 用/是/为`, `我习惯/喜欢/偏好`, `请/帮我` + verb) and English (`from now on`, `always/never/usually` + preference verb, `I prefer/usually/like/want to ...`, `default to ...`, `please always/never ...`).

`remember` is now gated by a new private `_remember_intent` that ORs `memory_in_use` with `preference_statement_intent`. `recall` / `forget` keep `memory_in_use` alone — those are explicit user actions, not LLM-initiated.

### Design alternative rejected

Making `remember` always-on. It blew Phase 2's context budget:

| Scenario | Before | After (always-on) | Budget |
|---|---|---|---|
| baseline | ~8000 chars | 10210 (+27%) | 8000 |
| realistic sc-de | ~12500 chars | 14931 (+20%) | 12500 |

The OR-predicate route keeps `remember` lazy-loaded so default-baseline cost is unchanged.

### Files changed

| File | Purpose |
|---|---|
| `omicsclaw/runtime/predicates.py` | Add `_PREFERENCE_STATEMENT_RE` regex + `preference_statement_intent()` |
| `omicsclaw/runtime/tool_predicates.py` | Add `_remember_intent` (OR-composition); switch `TOOL_PREDICATE_MAP["remember"]` to use it |
| `tests/test_predicates.py` | 5 unit tests: ZH-fires / EN-fires / false-positive probes / empty / acceptable-overfire boundary doc |
| `tests/test_tool_list_lazy_exposure.py` | End-to-end parametrize (5 preference queries × {remember appears, recall/forget hidden}) |

## Test plan

- [x] `pytest tests/test_predicates.py` — 48 passed (4 new unit tests + 1 boundary doc test)
- [x] `pytest tests/test_tool_list_lazy_exposure.py` — 86 passed (10 new parametrize cases)
- [x] `pytest tests/test_predicate_gated_injectors.py` — 29 passed
- [x] Wider regression: `pytest tests/test_tool_list_snapshots.py tests/bot/ tests/memory/ tests/test_bot_core_timeout.py` — 514 pass overall
- [x] TDD discipline: RED proven before GREEN at both layers (predicate + tool exposure)
- [x] Probed regex against 25 false-positive vectors including `"以后再说"`, `"the cells are always changing"`, `"默认值"`, `"I prefer the second option"`, `"一直跑不通"` — all correctly rejected

## Telemetry note

`predicate_hit / predicate_miss` events for `remember` now bucket under `_remember_intent` instead of `memory_in_use`. Any dashboard aggregating memory-keyword triggers will see the `remember` slice break out separately.

## Known pre-existing failure (out of scope)

`tests/test_tool_list_snapshots.py::test_realistic_scde_tool_list_under_phase2_budget` fails (12662 chars vs 12500 budget, +162 chars / +1.3%). **Pre-existing on `upstream/main` `b32540e` before any changes here** — confirmed by stashing my work and re-running. Worth filing a separate cleanup issue to either shave a tool description or revisit the Phase 2 budget.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * The system now recognizes when you express persistent preferences (e.g., "I prefer," "from now on") and automatically enables the remember tool. Supports both English and Chinese preference statements.

<!-- review_stack_entry_start -->

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/203)

<!-- review_stack_entry_end -->

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b32540e5b4e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.