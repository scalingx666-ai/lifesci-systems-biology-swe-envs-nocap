# Issue

**Title:** refactor(memory): route MemoryClient.forget through MemoryEngine

## Description

## Summary

Slice 2 of the §6.2 GraphService retirement. Adds `MemoryEngine.delete` and switches `MemoryClient.forget` off `GraphService.remove_path`. After this and slice 1 (PR #143), the only `MemoryClient` method still on the legacy `GraphService` is gone — only the four desktop server endpoints remain (slice 3).

- `MemoryEngine.delete(uri, *, namespace) -> dict` — subtree cascade with orphan prevention.
- Soft semantics preserved: Memory rows on the deleted node are marked `deprecated=True`, not physically removed, so the review pane and `ReviewLog.rollback_to` can resurrect them.
- Audit shape `{rows_before, rows_after}` is byte-equivalent, so `MemoryClient.forget`'s `snapshot.get_changeset_store().record_many(...)` call keeps working unchanged.
- One strictness improvement: the new `_delete_cascade_edge` helper is namespace-required (the legacy variant accepted `namespace=None` for admin tooling). Defense-in-depth — `engine.delete`'s only call site always forwards a namespace.

## Why slice this small

`graph.remove_path` is genuinely the most complex GraphService method: subtree path delete, orphan precheck, edge GC, soft node GC, search refresh, audit collector. Replicating it in the engine is ~250 LOC of careful porting; mixing this with the simpler `get_recent` swap (slice 1) or the rich UI dict shapes of the server endpoints (slice 3) would have been a bigger PR for no review benefit.

## Tests

7 new TDD tests in \`tests/memory/test_engine_delete.py\`:
- \`test_delete_removes_single_path\`
- \`test_delete_refuses_when_children_would_orphan\`
- \`test_delete_strict_namespace\`
- \`test_delete_soft_deprecates_memories\` — verifies Memory rows survive as deprecated
- \`test_delete_raises_on_missing_path\`
- \`test_delete_raises_on_root_path\`
- \`test_delete_returns_audit_dict\`

Existing namespace-isolation forget tests (`test_forget_does_not_delete_other_namespace_path`, `test_forget_routes_shared_prefix_uris_to_shared`) continue to pass with `engine.delete` underneath — they were always written against the surface contract, not the GraphService implementation path.

Memory regression suite: **301 passed**, zero regressions.

## Stacking

This PR branches from \`main\`, not from PR #143, but they touch independent regions of \`engine.py\` (`get_recent` is appended after `get_subtree`; `delete` is inserted near the other write verbs). Merge order doesn't matter; the import line in `engine.py` will need a trivial conflict resolution if both are merged.

## Test plan

- [x] 7 RED → GREEN tests for engine.delete
- [x] Memory regression suite: 301 passed
- [x] 5-axis code review — no blockers, atomicity verified, faithful contract reproduction confirmed
- [ ] Reviewer to confirm: orphan-check semantics match expectation (refuses parent delete if children only have under-prefix Paths — same as legacy)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7655db540527`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.