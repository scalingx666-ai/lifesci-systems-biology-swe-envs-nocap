# Issue

**Title:** refactor(memory): route MemoryClient.get_recent through MemoryEngine

## Description

## Summary

Slice 1 of the §6.2 GraphService retirement. Adds `MemoryEngine.get_recent` and switches `MemoryClient.get_recent` off `GraphService.get_recent_memories`. After this PR, the only call sites still hitting `GraphService` from the production client are `MemoryClient.forget` and the four desktop-UI server endpoints — both blocked on follow-ups (subtree cascade + rich UI dict shapes).

- `MemoryEngine.get_recent(*, namespace, limit=10, include_shared=False)` — strict by default; `include_shared=True` is the desktop UI mode.
- Output dict shape (`memory_id`, `uri`, `priority`, `disclosure`, `created_at`) matches legacy `GraphService.get_recent_memories` so callers need no changes.
- `MemoryClient.get_recent` now delegates straight to engine — one fewer GraphService instantiation per call.

## Why slice this small

Each remaining `GraphService` call site has its own complication:
- `MemoryClient.forget` needs subtree cascade + orphan prevention that `ReviewLog.cascade_delete` doesn't yet replicate.
- Server `/memory/{update,children,domains}` return rich dicts (`content_snippet`, `approx_children_count`, `rows_before`/`rows_after`) that are tied to the desktop UI contract.

`get_recent` has neither blocker — the dict shape is small and the strict-namespace semantics already match what `MemoryClient` documents — so it's the cleanest first step.

## Tests

5 new TDD-RED→GREEN tests in `tests/memory/test_namespace_isolation.py`:
- `test_engine_get_recent_strict_namespace`
- `test_engine_get_recent_include_shared`
- `test_engine_get_recent_return_shape`
- `test_engine_get_recent_honors_limit`
- `test_engine_get_recent_excludes_deprecated`

Full memory regression suite: 299 passed.

## Test plan

- [x] `tests/memory/` 5 new tests RED before implementation, GREEN after
- [x] `tests/memory/ tests/bot/test_session.py tests/test_app_server.py tests/integration/test_memory_cross_surface.py` — 299 passed
- [x] 5-axis code review — no blockers
- [ ] Reviewer to confirm: dict-shape parity with legacy is intentional (next slices keep callers shape-stable)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7cbe43250b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.