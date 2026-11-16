# Issue

**Title:** refactor(memory): route desktop /memory/{update,children,domains} through MemoryEngine

## Description

## Summary

Slice 3 of three for the §6.2 GraphService retirement. After this PR plus slices 1 (#143) and 2 (#145), no \`MemoryClient\` method and no \`omicsclaw/app/server.py\` endpoint reaches \`GraphService\` anymore. graph.py survives only behind the explicit \`oc memory-server\` admin routes in \`omicsclaw/memory/api/{browse,maintenance,review}.py\`, which intentionally keep \`namespace=None\` admin mode.

- \`MemoryEngine.list_children_rich\` — desktop-tree dicts with \`content_snippet\`, \`priority\`, \`disclosure\`, \`approx_children_count\`, alias-priority path picking, ROOT + \`context_domain\` filter, base64 self-heal. Faithful port of \`GraphService.get_children\`.
- \`MemoryEngine.list_paths\` — flat catalog with scoped-view dedupe by \`(domain, path)\` and namespace-matched-first ordering. Faithful port of \`GraphService.get_all_paths\`.
- \`MemoryClient.update_existing\` — pre/post audit snapshot + delegates to \`engine.upsert_versioned\` (content) or \`engine.patch_edge_metadata\` (metadata-only). Reproduces \`GraphService.update_memory\`'s wire shape; the two-element \`rows_after[\"memories\"]\` is intentional and documented (desktop review pane parses both sides of the chain transition).
- \`/memory/update\`, \`/memory/children\`, \`/memory/domains\` switched to the new \`MemoryClient\` methods.

## Slice 3 vs slice 1 + 2

This PR is independent of #143 and #145 — different methods, no overlapping line edits. The three slices can merge in any order; \`engine.py\` import lines are the only spot that needs trivial conflict resolution if all three land.

A small follow-up will switch \`/memory/recent\` to the engine once #143 (which adds \`engine.get_recent\`) merges. Trivial — ~5 LOC at the server endpoint.

## Tests

8 new TDD tests in \`tests/memory/test_engine_browse.py\`:
- \`test_list_children_rich_returns_rich_dicts\`
- \`test_list_children_rich_strict_namespace\`
- \`test_list_children_rich_include_shared\`
- \`test_list_children_rich_approx_children_count\`
- \`test_list_paths_returns_flat_list\`
- \`test_list_paths_strict_namespace\`
- \`test_list_paths_include_shared_dedupes\`
- \`test_list_paths_filter_by_domain\`

The existing PR #137 / #139 characterization tests at \`tests/memory/test_namespace_isolation.py\` and \`tests/test_app_server.py\` continue to pass — they were always written against the surface contract, not the GraphService implementation path.

Memory + app_server suite: **271 passed**, zero regressions.

## Test plan

- [x] 8 RED → GREEN tests for engine browse verbs
- [x] All endpoint characterization tests (\`test_app_server.py\` /memory/* tests) pass on top of the swap
- [x] 5-axis code review — atomicity verified, audit shape preserved, namespace strictness preserved
- [x] Defensive Query() normalisation in \`/memory/children\` so direct in-process calls match HTTP behaviour
- [ ] Reviewer to confirm: two-element \`rows_after[\"memories\"]\` shape is what the desktop review pane consumes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Enhanced memory browsing with rich child node details including content snippets, priority levels, and approximate descendant counts
  * New flat domain and path listing capabilities with complete metadata including priority and node identifiers
  * Improved support for shared content across memory namespaces

* **Tests**
  * Added comprehensive test coverage for memory browsing and listing operations

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/146)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2ac2f1f1e21`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.