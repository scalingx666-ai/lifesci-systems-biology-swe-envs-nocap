# Issue

**Title:** feat(memory): migrations framework + 001_namespace schema migration (PR #2)

## Description

## Summary

PR #2 of the 8-PR memory-system refactor. Adds a lightweight migrations framework and the first migration that introduces the ``namespace`` partition column.

**8 commits → 1047 LOC added across 8 new files, 1 file modified.** Independent of PR #1 (#125) — no overlapping imports.

## What lands

- **Migrations framework** (`omicsclaw/memory/migrations/{__init__,runner}.py`)
  - `_schema_version` table created on first invocation
  - `run_pending(db)` discovers ``NNN_*.py`` modules, sorts by version, applies pending ones
  - Idempotent at framework level (skips already-applied versions)
  - Failed `apply()` leaves `_schema_version` untouched

- **`init_db()` wiring** (`omicsclaw/memory/database.py:140`)
  - After `Base.metadata.create_all`, `await run_pending(self)` is invoked
  - Deferred import prevents a circular dependency at module load time

- **`001_namespace` migration** (`omicsclaw/memory/migrations/001_namespace.py`)
  - Adds ``namespace VARCHAR(128) NOT NULL DEFAULT '__shared__'`` to `paths`, `search_documents`, `glossary_keywords`
  - Rebuilds `paths` PK to `(namespace, domain, path)`
  - Rebuilds `search_documents` PK to `(namespace, domain, path)`
  - Rebuilds `glossary_keywords` UNIQUE to `(namespace, keyword, node_uuid)`
  - Drops + recreates `search_documents_fts` virtual table with the namespace column, repopulating from rewritten search_documents
  - Best-effort backfill of namespace from `disclosure` field — extracts `(platform, user_id)` from both formats:
    - `Memory from session <platform>:<user_id>:<session_id>` (memory rows)
    - `Session for user <user_id> on <platform>` (session rows)
  - Idempotent: a column-existence guard on `paths.namespace` short-circuits re-runs, preserving any post-migration namespace edits

- **Production-data dry-run script** (`scripts/migrate_dry_run.py`)
  - Copies a memory.db to a temp path and runs migrations against the copy
  - Reports row-count diff, namespace distribution, count of unparseable disclosures
  - Exit code 0 only if row counts are preserved
  - Original DB is never touched

## Verified against live data

```
Source: ~/.config/omicsclaw/memory.db (220KB, 42 paths)

Row counts (preserved across all 6 tables):
  nodes 43 · memories 108 · edges 42 · paths 42
  search_documents 42 · glossary_keywords 0

Namespace distribution (paths) after migration:
  app/desktop_user  35
  __shared__        3
  cli/cli_user      2
  tui/tui_user      2

Unparseable disclosures: 0
```

A backup `memory.db.pre-pr2.bak` was taken before testing; md5 verified unchanged after dry-run.

## Risk

- **Schema migration → high-risk PR**, but mitigated by:
  - Idempotent guard makes the migration safe to re-run
  - Drop+recreate pattern is the standard SQLite approach for PK/constraint changes
  - 22 new tests cover idempotency, row-count preservation, backfill correctness, FTS rebuild, end-to-end via init_db
  - Dry-run validated against the actual production DB
- **Existing memory tests unaffected**: `test_scoped_memory.py` (3) + `test_memory_server_security.py` (5) continue to pass
- **No ORM model changes** in this PR — `models.py` still describes the pre-migration schema. The new schema works because all writes default to `namespace='__shared__'`, the SQLAlchemy ORM ignores the extra column, and PR #3 will update models.py when the engine actually exercises the namespace column

## Test plan

- [x] `pytest tests/memory/` — 22/22 pass (6 runner + 2 init_db + 14 migration_001)
- [x] `pytest tests/test_scoped_memory.py tests/test_memory_server_security.py` — 8/8 pass
- [x] `python scripts/migrate_dry_run.py` against ~/.config/omicsclaw/memory.db — clean, all assertions match
- [x] Backup md5 verified unchanged after dry-run

## Follow-ups (not blocking)

- PR #3 (MemoryEngine + SearchIndexer) will update `models.py` to add namespace columns to the ORM models. Until then, the schema and ORM diverge harmlessly because every write defaults to `__shared__`.
- Backfill loop is O(N) UPDATEs — fine for current 42-row scale; would need batching at 10K+ rows.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added namespace support to the database, enabling improved data organization and isolation across storage tables.
  * Implemented an automated migration framework to safely apply and track database schema changes.

* **Tests**
  * Added comprehensive test coverage for migration execution, schema transformations, and namespace functionality.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/126)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13c7564af9f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.