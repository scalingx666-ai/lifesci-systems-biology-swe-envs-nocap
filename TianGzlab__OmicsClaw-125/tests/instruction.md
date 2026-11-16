# Issue

**Title:** feat(memory): add MemoryURI + namespace_policy (PR #1 of memory refactor)

## Description

## Summary

PR #1 of an 8-PR memory-system refactor. **Pure-addition foundation** — 4 new files, 0 modifications, 0 deletions.

- `omicsclaw/memory/uri.py` — `MemoryURI` value object (62 lines)
- `omicsclaw/memory/namespace_policy.py` — `resolve_namespace`, `should_version` pure functions (52 lines)
- `tests/memory/test_memory_uri.py` — 20 tests covering all invariants
- `tests/memory/test_namespace_policy.py` — 23 tests including a parametrized matrix locking the namespace ownership table

## Why

The existing memory module has three duplicated `_parse_uri` helpers (`memory_client.py:32`, `snapshot.py:349`, `compat.py:184`). PR #1 introduces shared layer-0/1 vocabulary that subsequent PRs build on:

1. **`MemoryURI`** — single immutable value object: `parse`/`str` roundtrip, `parent()/child()/root()` navigation, validated invariants (`__post_init__` rejects empty domain, `://` in domain or path, control chars in domain).
2. **`namespace_policy`** — pure-function classification along two independent axes:
   - `resolve_namespace(uri, current=N)` → `"__shared__"` (system content) or `N` (user/workspace namespace)
   - `should_version(uri)` → `True` for URIs requiring deprecation chains (preferences, agent identity)

These unblock subsequent PRs that introduce the migration framework, the new `MemoryEngine` (hot path), and `ReviewLog` (cold path).

## Namespace ownership (locked via parametrized matrix test)

| URI form | namespace | versioned |
|---|---|---|
| `core://agent` | `__shared__` | ✅ |
| `core://kh/*` | `__shared__` | ❌ |
| `core://my_user_default` | `__shared__` | ❌ |
| `core://my_user` | per-namespace | ✅ |
| `preference://*` | per-namespace | ✅ |
| `dataset://*`, `analysis://*`, `insight://*`, `project://*`, `session://*` | per-namespace | ❌ |

Future edits to `SHARED_PREFIXES` / `VERSIONED_PREFIXES` must keep the matrix test green.

## Risk

- **Pure addition** — 0 existing files modified
- **51 targeted tests green** (43 new + 8 existing memory-related)
- **Wide suite**: 2039 pass / 12 fail; all 12 failures **preexisting on main** (verified by running them against main; failing tests are in unrelated subsystems — KnowHow ranking, OAuth, provider registry, prompt snapshots, tool list predicate — none import `omicsclaw.memory`)
- **Rebased** onto latest main (post-#124); rebase clean, no conflicts

## Test plan

- [x] `pytest tests/memory/` — 43/43 pass
- [x] `pytest tests/test_scoped_memory.py tests/test_memory_server_security.py` — 8/8 pass
- [x] Rebased onto `13c7564`; 43 memory tests still green post-rebase

## Follow-ups (not blocking)

- Optional: validate path control chars (currently only domain validates) — defer to PR #6 cleanup
- Optional: `parse(None)` could raise `TypeError` with clearer message
- PR #6 cleanup will migrate the 3 existing `_parse_uri` call sites to `MemoryURI.parse`

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13c7564af9f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.