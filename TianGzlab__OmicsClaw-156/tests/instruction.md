# Issue

**Title:** fix(memory): /memory/browse children must use rich shape

## Description

## Summary

- `/memory/browse` was still calling `MemoryClient.list_children` (sparse
  `MemoryRef`: `memory_id`, `node_uuid`, `namespace`, `uri`) after PR #146
  switched the parallel `/memory/children` endpoint to `list_children_rich`.
- Desktop UI (`MemoryTree.tsx`, `MemoryContent.tsx`) reads
  `name`/`path`/`domain`/`approx_children_count` to render labels and the
  directory-vs-leaf icon — without those fields every child rendered as a
  blank row (regression visible after the desktop backend was restarted to
  pick up post-#146 code).
- Switch `/memory/browse` to `list_children_rich(context_domain,
  context_path, include_shared=True)` — same call shape `/memory/children`
  already uses, including `__shared__` visibility.

## Test plan

- [x] New TDD test `test_memory_browse_children_have_rich_shape` —
      reproduces the regression on the sparse shape, passes after the fix
- [x] All five `memory_browse` tests green (existing + new)
- [x] Full memory regression suite green: `tests/memory/`,
      `tests/test_app_server.py`, `tests/integration/test_memory_cross_surface.py`,
      etc. — 318 passed
- [ ] Manual verification in `electron:dev`: child names render in the
      Memory tree and right-pane "Children (N)" list, History button still
      shows on `core://my_user/*` after PR #153

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd6ee37f2b2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.