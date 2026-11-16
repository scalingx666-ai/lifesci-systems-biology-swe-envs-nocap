# Issue

**Title:** refactor(memory): route /api/maintenance through ReviewLog (Phase 2a)

## Description

## TL;DR
Phase 2a of the GraphService retirement plan. `api/maintenance.py` is the smallest of the three cold-path API modules that still imported `get_graph_service()`. This PR adds three new `ReviewLog` methods (mirroring the legacy dict-shaped contract) and rewires the maintenance endpoints to use them. The legacy GraphService methods stay alive for now — Phase 3 deletes the class once `review.py` and `browse.py` also migrate.

## Recommended review order

1. `omicsclaw/memory/review_log.py` — new public methods (`list_orphans_with_chain`, `get_orphan_detail`, `permanently_delete_orphan`) + helpers (`_resolve_migration_chain`, `_collect_and_clear_memoryless_node`)
2. `omicsclaw/memory/api/maintenance.py` — full rewrite, now 65 lines, zero `GraphService` references
3. `tests/memory/test_review_log_orphan_chain.py` — 12 tests pinning shape parity + edge cases

## Diff buckets

| Bucket | Files | Why |
|---|---|---|
| New API on ReviewLog | `review_log.py` | Absorb the maintenance contract off GraphService |
| Surface rewire | `api/maintenance.py` | Delegate endpoints to ReviewLog |
| Tests | `test_review_log_orphan_chain.py` (12 cases) | Lock dict shape + node-GC semantics |

## Key design decisions

- **Dict-shaped output preserved verbatim.** Frontend consumes `id, content_snippet, deprecated, migrated_to, category, migration_target` — every key matches GraphService field-for-field.
- **Snippet truncation at 200 chars + `...` trailer** — same constant the legacy used; one named constant `_SNIPPET_LIMIT` for future tuning.
- **Conservative node GC.** When `permanently_delete_orphan` empties a node, the new helper clears only that node's direct edges/paths/glossary. The legacy `cascade_delete_node` would recursively descend into children — that path is reachable from an admin button, so the more conservative semantics avoid ever wiping unrelated descendants. A test pins the contract.
- **Helpers are private to ReviewLog.** No new module, no cross-import with GraphService — Phase 3's deletion target stays clean.

## Risk notes

- Behaviour divergence: `permanently_delete_orphan` no longer recursively deletes children of a memoryless node. Tested guard. The only place this could change observable behaviour is if the admin pane ever deletes an orphan whose node still has active children — extremely uncommon, and arguably safer than the legacy nuke.
- No frontend changes expected. JSON shape is identical and verified by `test_list_orphans_with_chain_returns_dict_shape`.

## Verification

- 12 new ReviewLog tests pass
- 262 full memory test suite still green
- 114 bot + app suite still green
- `grep -n GraphService omicsclaw/memory/api/maintenance.py` → 0 hits

## Out of scope (follow-ups)

- Phase 2b: migrate `api/review.py` to ReviewLog (4 GraphService calls)
- Phase 2c: migrate `api/browse.py` to MemoryEngine (8 calls, includes write paths)
- Phase 3: delete `graph.py` (`GraphService` class + `get_graph_service` factory)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53ac75205e6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.