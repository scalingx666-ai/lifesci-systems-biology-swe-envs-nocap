# Issue

**Title:** refactor(memory): route /api/review through ReviewLog (Phase 2b)

## Description

## TL;DR
Phase 2b of the GraphService retirement plan. After this PR, `api/review.py` no longer imports `get_graph_service`. Two new `ReviewLog` methods absorb the diff-content lookup and the path-restoration rollback; the path-creation rollback routes straight to `MemoryEngine.delete`.

## Recommended review order

1. `omicsclaw/memory/review_log.py` — new public methods (`get_memory_by_id`, `restore_path`)
2. `omicsclaw/memory/api/review.py` — full rewrite, zero `GraphService` references
3. `tests/memory/test_review_log_rollback_api.py` — 7 tests pinning shape + guard contracts

## Diff buckets

| Bucket | Files | Why |
|---|---|---|
| New ReviewLog API | `review_log.py` | get_memory_by_id + restore_path |
| Surface rewire | `api/review.py` | Route /diff, /rollback off GraphService |
| Tests | `test_review_log_rollback_api.py` (7 cases) | Lock contract + guards |

## Key design decisions

- **`rollback_to` namespace param is unused inside the chain rewrite.** Passing `__shared__` from `/api/review/rollback` is a no-op semantically but satisfies the typed signature. The legacy `rollback_to_memory` took no namespace; ReviewLog's signature was hardened earlier without altering body logic, so the migration is contract-preserving.
- **Path namespace recovery from the changeset.** The legacy rollback ignored namespace (admin-unfiltered). The new path tries `before.get("namespace", "__shared__")` so rollbacks land on the right partition when the snapshot carries it.
- **Edge lookup before `restore_path`.** A deleted path's edge may be GC'd too. We look up the original edge via the snapshotted `edge_id`; if it's gone, the rollback reports "Edge not found" rather than guessing. Matches the legacy behaviour.

## Risk notes

- `/rollback` for memories rollback is now namespace-typed via `rollback_to`. Verified the body doesn't consult `namespace`, so passing `__shared__` does not skew which memory gets restored.
- `/rollback` for path-creation now derives namespace from the snapshot. If a future snapshot serializer drops the field, the default `__shared__` keeps behaviour bug-compatible with the legacy.
- All 7 endpoint tests under `tests/test_app_server.py::test_memory_review_*` still pass.

## Verification

- 7 new ReviewLog tests pass
- 384 tests across memory/bot/app suites still green
- `grep -n "GraphService\|get_graph_service" omicsclaw/memory/api/review.py` → 0 hits

## Out of scope (follow-ups)

- Phase 2c: migrate `api/browse.py` to MemoryEngine (8 GraphService calls, includes write paths like `create_memory` / `add_path` that need careful shape preservation)
- Phase 3: delete `graph.py` (`GraphService` class + `get_graph_service` factory + `_graph_service` singleton)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4793fb59011`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.