# Issue

**Title:** feat(memory): expose is_versioned in /memory/browse response

## Description

## Summary

The desktop UI needs to decide whether to show a "History / Roll back" button on a memory view. The decision is purely based on \`namespace_policy.should_version(uri)\`: \`core://agent/*\`, \`core://my_user/*\`, and \`preference://*\` URIs have version chains; everything else is overwrite-only.

Rather than duplicate the rule on the frontend, this PR adds an \`is_versioned: bool\` field to the \`/memory/browse\` response. Single source of truth on the server; frontend reads the flag.

**Slice 1 of 2** for the version-chain history feature. Slice 2 in the OmicsClaw-App repo wires the flag to a History modal + rollback button.

## Tests

3 new tests in \`tests/test_app_server.py\`:
- versioned URI (\`core://my_user/note\`) → \`is_versioned=true\`
- overwrite URI (\`dataset://x.h5ad\`) → \`is_versioned=false\`
- root browse (\`path=""\`, \`domain="core"\`) → field present, value \`false\` (root has no record)

Memory + app_server suite: 298 passed.

## Stat

+102 / -0 across 2 files.

## Test plan

- [x] 3 RED → GREEN tests for is_versioned
- [x] Existing /memory/browse tests still pass (read fallback, namespace isolation)
- [x] Memory regression suite: 298 passed
- [x] 5-axis code review — no blockers, single source of truth preserved
- [ ] Reviewer to confirm: \`is_versioned\` at the HTTP boundary (not on \`MemoryClient\`/\`MemoryEngine\`) is the right layer — argument is "UI-shaped concern lives on the wire"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee42d6c303c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.