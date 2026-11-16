# Issue

**Title:** refactor(memory): route /memory/recent through MemoryEngine

## Description

## Summary

Trivial follow-up that closes the §6.2 GraphService retirement. After slices 1 (#143), 2 (#145), 3 (#146), \`/memory/recent\` was the last GraphService caller in \`omicsclaw/app/server.py\`. This PR:

- Adds an \`include_shared\` kwarg to \`MemoryClient.get_recent\` (default \`False\` — backward-compatible with the 2 existing callers).
- Switches \`/memory/recent\` to call \`_memory_client.get_recent(limit=limit, include_shared=True)\`.
- Drops the now-dead \`_get_graph_service\` helper from \`server.py\`.

After merge, no production code in \`MemoryClient\` or \`omicsclaw/app/server.py\` touches \`GraphService\`. \`graph.py\` survives only behind the explicit \`oc memory-server\` admin routes in \`omicsclaw/memory/api/{browse,maintenance,review}.py\`, which intentionally keep \`namespace=None\` admin mode.

## Tests

- Existing endpoint test \`test_memory_recent_endpoint_excludes_other_namespaces\` (PR #137 / #139) passes on the new path — the desktop's own writes + \`__shared__\` rows surface, bystander writes don't leak.
- Existing strict-namespace contract tests (\`test_get_recent_only_returns_own_namespace\`, \`test_get_recent_excludes_shared_rows\`) still hold — \`get_recent\` strict default is unchanged.
- Engine-level \`include_shared\` semantics already tested by \`test_engine_get_recent_include_shared\` (added in slice 1, PR #143).
- Memory + app_server suite: 295 passed.

Diff: 23 insertions / 22 deletions.

## Test plan

- [x] Existing /memory/recent endpoint test passes on engine path
- [x] Strict-namespace get_recent tests still pass (backward compat verified)
- [x] No production calls to GraphService remain in MemoryClient or app/server.py
- [ ] Reviewer to confirm: include_shared kwarg default-False is the right backward-compat choice (alternative: new method \`get_recent_with_shared\`, but kwarg keeps the API surface tighter)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4e125478e33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.