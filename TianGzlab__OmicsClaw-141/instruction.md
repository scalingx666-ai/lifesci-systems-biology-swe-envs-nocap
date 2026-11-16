# Issue

**Title:** fix(memory): CompatMemoryStore self-initialises on first public async call

## Description

## Summary

Production bug discovered while testing the memory system from the CLI:

```
CALL #4  remember({"memory_type": "preference", "key": "language", "value": "zh"})
ERROR: Memory save failed: CompatMemoryStore must be initialised before use
  File "bot/tool_executors.py:1391" in execute_remember
    mem_id = await _core.memory_store.save_memory(session_id, pref)
  File "omicsclaw/memory/compat.py:283" in _client
    assert self._session_client is not None, (
AssertionError: CompatMemoryStore must be initialised before use
```

## Root cause

`bot/session.py:init()` is a **synchronous** bootstrap. It constructs the store and assigns to `bot.core.memory_store` but cannot `await` the async `initialize()` coroutine that builds the `DatabaseManager` / `MemoryEngine` / `SearchIndexer` / shared `_session_client`. The very first LLM tool call (`execute_remember` → `save_memory`) therefore reaches the `_client` property's `assert self._session_client is not None` and blows up.

The `_assemble_chat_context` flow that runs before tool calls happens to wrap `session_manager.get_or_create` in `try/except Exception`, which silently swallows the same AssertionError and lets the chat continue session-less. The error only surfaces when the LLM later issues a `manage_memory` tool call where there's no broad swallow.

## Fix

Every public async method on `CompatMemoryStore` now begins with `await self.initialize()`. The method is already idempotent (`if self._initialized: return`), so the cost is one bool check per call after the first.

Methods touched (7):
- `create_session`, `get_session`, `save_memory`, `get_memories`, `update_memory`, `delete_session`, `search_memories`

`update_session`, `load_context`, `cleanup_expired` transitively reach init via these or are no-ops.

## Why my T1/T2 coverage missed this

Every test fixture in tests/memory/, tests/bot/, tests/integration/ explicitly awaited `store.initialize()` before yielding, masking the production init gap entirely. This PR adds a regression test that mirrors the actual bot init path — store created sync, `initialize()` never awaited — so any future re-introduction of the gap is caught immediately.

## Test plan

- [x] `tests/memory/test_compat_namespace.py::test_compat_store_lazy_initialises_on_first_public_call` — RED before fix (reproduces the user-reported AssertionError verbatim), GREEN after.
- [x] Curated regression: **325/325** in tests/memory/ + tests/bot/ + tests/test_app_server.py + tests/integration/test_memory_cross_surface.py + adjacent files (was 324 pre-PR; +1 new lazy-init test).
- [ ] CI green
- [ ] Verify in CLI: `oc interactive` → ask "记住我用中文回答" → expect ✓ Preference saved (instead of the AssertionError trace from the bug report)

## Production impact

The user's prior CLI memory tool call **did not persist** (bug prevented the write). After this lands, re-issuing the same request will succeed. No DB cleanup needed — the failed call left no rows behind.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3caa62c2231b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.