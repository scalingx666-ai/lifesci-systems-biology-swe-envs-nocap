# Issue

**Title:** fix(memory): close cross-namespace data-loss + info-leak holes in legacy GraphService entrypoints

## Description

## Summary

Verification of the PR #125–#134 memory refactor turned up a family of real bugs: the 5 legacy `GraphService` methods still called from `MemoryClient.forget`, `MemoryClient.get_recent`, and three desktop `/memory/*` endpoints had **no namespace filtering**. Same SQL pattern as the PR #131 GC data-loss bug.

| # | Bug | Severity |
|---|---|---|
| **D2** | `MemoryClient.forget(uri)` could delete another user's `(domain, path)` row — cross-namespace data loss | Critical |
| **D2'** | `MemoryClient.get_recent()` returned recent memories from EVERY namespace | Critical (privacy) |
| **D3** | `/memory/children` returned cross-namespace children to the desktop UI | High (info leak) |
| **D3'** | `/memory/domains` mixed counts across namespaces and dedup'd them away | Medium (incorrect counts + leak) |
| **5th site** | `/memory/update` was hardcoded to `Path.namespace == SHARED_NAMESPACE` — desktop users could never edit their per-namespace memories | High (broken feature) |
| **D1** | `app/server.py` hardcoded `user_id="desktop_user"` for chat while `desktop_namespace()` reads `OMICSCLAW_DESKTOP_LAUNCH_ID`. Multi-launch deployments wrote chat memories to a namespace the endpoints couldn't read | High (silent under default; bites multi-launch) |
| **D5** | `CompatMemoryStore._client_for_session` silently fell back to `__shared__` when a session was missing — auto-captured datasets arriving before session creation leaked globally | Medium (privacy) |

## Approach

Add `namespace=` (and `include_shared=` where UX requires it) to the 5 `GraphService` methods. `namespace=None` preserves the legacy unfiltered admin path used by `oc memory-server`'s browse routes (`omicsclaw/memory/api/browse.py`) — zero changes needed there.

`MemoryClient.forget` routes via the same `namespace_policy.resolve_namespace()` as `MemoryClient.remember()`, so shared-prefix URIs (`core://agent/*`, `core://kh/*`) stay **symmetric** — a per-user client can clean up its own shared writes — while non-shared URIs cannot reach other namespaces.

Desktop endpoints (`/memory/children`, `/memory/domains`, `/memory/recent`) pass `include_shared=True` so the single-user UI tree shows user-customized `__shared__` rows alongside per-namespace rows. Strict default keeps multi-tenant bot inventories clean.

Cascade chain (`_cascade_delete_edge`, `_gc_node_soft`) also threads `namespace` through, encoding the invariant on the helpers themselves so a future caller can't re-introduce the cross-namespace cascade by accident.

`CompatMemoryStore._client_for_session` now raises `LookupError` instead of falling back to `__shared__`. All three callers (`save_memory`, `get_memories`, `search_memories`) sit inside `try/except` wrappers in production callers (`_auto_capture_dataset`, etc.) so the error is contained as a logged skip — never as a privacy leak.

## Test plan

- [x] 13 new tests in `tests/memory/test_namespace_isolation.py` (red→green map in module docstring)
  - Cross-namespace forget data loss (D2)
  - Shared-prefix forget symmetry (D2 follow-up — caught at 5-axis review)
  - get_recent cross-namespace info leak (D2')
  - get_recent excludes `__shared__` rows by default (read-fallback boundary)
  - get_children / get_all_paths namespace filter (D3)
  - get_children / get_all_paths / get_recent_memories `include_shared=True` desktop UI mode
  - update_memory respects caller's namespace (5th site)
  - `_client_for_session` raises LookupError; `save_memory` propagates and writes nothing (D5)
  - Desktop chat user_id ↔ desktop_namespace invariant (D1)
- [x] Updated `tests/memory/test_compat_namespace.py::test_save_memory_with_unknown_session_raises` to pin the new contract (was `..._falls_back_to_shared`)
- [x] Curated regression suite from prior session: **283/283** (was 270 pre-fix; +13 isolation, +1 renamed compat test)
- [x] 5-axis review by code-reviewer agent — addressed 1 important blocker (forget asymmetry) + 1 important latent bug (`_cascade_delete_edge` namespace propagation) + 1 important UX (desktop `include_shared`) before commit
- [ ] CI green

## Out of scope

- `omicsclaw/memory/api/browse.py` (admin REST API for `oc memory-server`) keeps `namespace=None` legacy behavior — it's not in the user-facing entry layer.
- CLI/TUI is graph-unbound today (uses `ScopedMemory` only); a future PR can wire it via `cli_namespace_from_workspace` if cross-Surface continuity becomes a feature.
- Plan §6.2 acceptance "graph.py < 100 lines" remains unmet; full GraphService retirement is tracked as a follow-up (handoff Option B). This PR closes the bugs **without** that retirement.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f09e35fafc15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.