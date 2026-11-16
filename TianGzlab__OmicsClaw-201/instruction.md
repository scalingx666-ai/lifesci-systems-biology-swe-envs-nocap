# Issue

**Title:** feat(memory): add namespace override + admin view to /memory/domains

## Description

## Summary

Adds the contract the desktop admin/debug UI needs to inspect data written under stale or sibling namespaces (e.g. legacy `app/<launch-uuid>` partitions left behind before the LAUNCH_ID → USER_ID fix in #199).

## API

### `GET /memory/domains?namespace=<value>`
- **omitted** (default): desktop user's own namespace + `__shared__` — current behaviour, unchanged.
- **empty string** (`?namespace=`): admin view — every partition aggregated, deduped on `(namespace, domain, path)`.
- **concrete value** (`?namespace=app/foo`): inspect that partition + `__shared__`.

### `GET /memory/namespaces` (new)
Returns `{namespaces: [...], current: \"app/desktop_user\"}` so an admin UI can render the dropdown and preselect the namespace `_memory_client` is bound to.

## Engine additions

- `MemoryEngine.list_paths(namespace=None, ...)` is the admin mode entry point — skip the namespace filter, dedupe on `(namespace, domain, path)`, ignore `include_shared` (shared rows already included).
- `MemoryEngine.list_namespaces()` returns every distinct partition that currently holds at least one path, sorted for stable UI display.

## Back-compat

`MemoryClient.list_paths` always passes a concrete namespace, so its callers (and the existing default-scope behaviour of `/memory/domains`) are unaffected by the engine signature widening.

## Test plan

- [x] `pytest tests/memory/test_engine_browse.py` — 11/11 pass (incl. 3 new engine tests)
- [x] `pytest tests/test_app_server.py -k memory` — 37/37 pass (incl. 3 new endpoint tests covering default, admin, explicit-namespace, plus 1 for `/memory/namespaces`)
- [x] Full memory suite — 283/283 pass

## Pairing

Pairs with the desktop UI work on https://github.com/zhou-1314/OmicsClaw-App — a namespace dropdown component will consume `/memory/namespaces` and pass the selection through to `/memory/domains?namespace=`. Backend lands first so the UI has a stable contract to build against.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `726dacb3b3b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.