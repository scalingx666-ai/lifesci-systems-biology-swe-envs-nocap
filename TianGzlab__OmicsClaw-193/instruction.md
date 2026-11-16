# Issue

**Title:** Phase 2 B1: zero out omicsclaw → bot reverse imports from sc_batch preflight

## Description

## Summary

Closes 4/16 of the lazy `omicsclaw/` → `bot/` reverse imports tracked in
the Phase 1 boundary guardrail (`tests/test_no_reverse_imports.py`).
`omicsclaw/runtime/preflight/sc_batch.py` is now **completely free** of
reverse imports — the engine-side single-cell preflight no longer
reaches back into `bot/` at runtime.

Approach: three thin slices, each landing as its own commit with the
ratchet lowered inline so intermediate states stay green.

1. **`refactor(runtime): lift _lookup_skill_info into omicsclaw.runtime.skill_lookup`** — pure registry walk, no bot state; `bot.skill_orchestration._lookup_skill_info` stays as a thin alias for backward compat. Ratchet 16 → 14.
2. **`refactor(runtime): lift skill-chain helpers into omicsclaw.runtime.skill_chain`** — `_normalize_extra_args`, `_run_skill_via_shared_runner`, `_run_omics_skill_step` all move to `omicsclaw/runtime/skill_chain.py`. The new `run_omics_skill_step` takes an explicit `output_root: Path` so the runtime side stays free of bot path constants; the bot adapter keeps the `OUTPUT_DIR` default. Ratchet 14 → 13.
3. **`refactor(preflight): invert control flow so sc_batch never re-enters execute_omicsclaw`** — `_auto_prepare_sc_batch_integration` now returns a control-signal dict (`None` / `{"final_message": str}` / `{"chained_args": ..., "summary_prefix": ...}`) instead of calling back into `bot.tool_executors.execute_omicsclaw`. The bot side consumes the dict and self-recurses with `auto_prepare=False`. Same observable behavior; engine side is strictly one-way. Ratchet 13 → 12, `sc_batch.py` drops off the allowlist.

## Why

Phase 1 (#192) shipped the boundary guardrail and a ratcheted allowlist
of 16 grandfathered lazy reverse imports. `omicsclaw/runtime/preflight/sc_batch.py`
held 4 of them and was the easiest win to attack first — the helpers
involved (`_lookup_skill_info`, `_run_omics_skill_step`,
`_run_skill_via_shared_runner`) were already 95% domain-agnostic; only
`OUTPUT_DIR` and one chain-tail callback were keeping them on the bot
side.

Lifting them out means:
- The single-cell preflight is now testable without any `bot/` import.
- `bot.skill_orchestration` shrinks ~140 LOC (mostly delegation aliases).
- Identity invariants from Phase 1 (`bot.core.X is bot.skill_orchestration.X`)
  are preserved — verified end-to-end.

The remaining 12 entries in the allowlist live in
`omicsclaw/app/server.py` (6) and `omicsclaw/interactive/{interactive,tui}.py` (6).
Both require larger architectural moves (lifting `CHANNEL_REGISTRY` /
`ChannelManager` to `omicsclaw/`, exposing a surface-agnostic engine
entry for interactive). Separate Phase 2 slices.

## Test plan

- [x] `tests/test_no_reverse_imports.py` — 3/3 green (top-level=0, lazy
      allowlist matches 12 real grandfathered sites, count pin 12).
- [x] Full Phase 1 regression: `tests/engine/ tests/bot/
      tests/test_bot_agent_loop_imports.py tests/test_compact_slash_command.py
      tests/test_channels.py` — 143 passed, 4 errors. The 4 errors are
      the pre-existing pydantic v1/v2 collection failures documented in
      the Phase 1 PR (`tests/bot/test_skill_orchestration.py` ×2 +
      `tests/bot/test_tool_executors.py` ×2). Confirmed unchanged.
- [x] Identity invariant: `bot.core._lookup_skill_info is bot.skill_orchestration._lookup_skill_info` — true.
- [x] sc_batch.py imports via `bot.core` entry order — no circular-import
      regression beyond the pre-existing bot.core ↔ bot.tool_executors
      pattern documented in `bot/tool_executors.py:11-25`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a04db2f9332`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.