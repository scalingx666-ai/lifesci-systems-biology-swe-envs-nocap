# Issue

**Title:** refactor(memory): retire GraphService class — Phase 2c + 3

## Description

## TL;DR
Closes Phase 2c (`api/browse.py` GraphService migration) and Phase 3 (delete `GraphService` class) of the memory refactor plan. `omicsclaw/memory/graph.py` is gone; its body now lives as a private `BrowseHelpers` class inside `omicsclaw/memory/api/_browse_helpers.py` consumed only by the `oc memory-server` admin UI.

## Recommended review order

1. `omicsclaw/memory/api/_browse_helpers.py` — file rename of `graph.py` (97% similarity by content); only the class name and relative imports changed
2. `omicsclaw/memory/api/browse.py` — endpoints now build a fresh `BrowseHelpers` per request via `_browse_helpers()` factory
3. `omicsclaw/memory/__init__.py` — `GraphService` re-export + `get_graph_service` factory + `_graph_service` singleton removed
4. `tests/test_app_server.py` — fixture updated to instantiate `BrowseHelpers` directly
5. `tests/memory/test_namespace_isolation.py` — DELETED (503 lines testing legacy GraphService stragglers)

## Diff buckets

| Bucket | Files | Why |
|---|---|---|
| File move + rename | `graph.py` → `api/_browse_helpers.py` | Make the class private; class name change documents legacy status |
| Factory removal | `omicsclaw/memory/__init__.py` | Drop GraphService from the import surface |
| API rewire | `api/browse.py` | Use `BrowseHelpers` locally instead of the deleted factory |
| Test cleanup | `test_app_server.py`, deleted `test_namespace_isolation.py` | Fixture update; obsolete namespace tests retired (coverage already in MemoryEngine/MemoryClient suites) |
| Docs | `AGENTS.md`, `omicsclaw/memory/__init__.py`, `_browse_helpers.py` header | Update migration note; signal future deletion |

## Key design decisions

- **Rename instead of rewrite.** The path-based admin contract (`/create`, PUT `/node`, `/add-path`, DELETE `/path`) has no clean MemoryEngine equivalent — engine is URI-based, admin UI is path+title-based. A rewrite is its own project; this PR achieves "GraphService gone" without taking on that scope.
- **Private module (`_browse_helpers.py`, leading `_`).** Class name change `GraphService` → `BrowseHelpers` plus the underscore prefix together signal "do not import from outside `omicsclaw/memory/api/`."
- **Per-request `BrowseHelpers` instantiation.** Constructor is three assignments + one `MemoryEngine()` build; cheap and stateless. No reason to singleton.

## Risk notes

- 367 tests pass. No frontend changes — same FastAPI routes, same JSON shapes, same Pydantic validation.
- Any external caller importing `from omicsclaw.memory import get_graph_service` now breaks loudly with `ImportError` — which is the desired migration signal.
- Deleted `test_namespace_isolation.py` was specifically pinning legacy GraphService stragglers. Equivalent invariants are already covered by `tests/memory/test_engine_*.py`, `test_memory_client.py`, `test_namespace_policy.py`, `test_search_indexer_namespace.py`.

## Verification

- `grep -rn "GraphService\|get_graph_service" omicsclaw/ --include="*.py"` → only docstring/comment lines remain (historical context)
- `grep -rn "from omicsclaw.memory.graph" omicsclaw/ tests/` → 0 matches
- 367/367 memory + bot + app tests pass
- 5-axis review pre-push: APPROVE (4 nits, all addressed)

## What's intentionally kept

- `_browse_helpers.py` carries ~1500 lines of path-based logic verbatim. The intent is that a future rewrite ports the admin UI against `MemoryEngine` and then deletes this module entirely. A TODO on the pyright suppression header sets that expectation.
- Several docstrings in `engine.py`, `review_log.py`, `memory_client.py`, `models.py` mention `GraphService` as historical context. Those are comments, not code references — harmless.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Documentation**
  * Updated memory system documentation with API architecture migration guidance and initialization flow clarification.

* **Refactor**
  * Restructured internal memory service layer components.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/175)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79eb50f9db83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.