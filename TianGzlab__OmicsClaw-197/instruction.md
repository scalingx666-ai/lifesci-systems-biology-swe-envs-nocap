# Issue

**Title:** feat(doctor): add graph memory subsystem health check

## Description

## Summary

`oc doctor` covered Session DB, Knowledge Index, Skill Catalog, Graphify, MCP, and workspace directories — but the **graph memory subsystem (`omicsclaw/memory/`) had no health probe**, despite owning its own SQLite database and being the focus of every recent refactor (Phase 2a → 2b → 2c → 3 in PRs #173–#175). A schema/migration/KH-bootstrap breakage had no surfaced signal.

This PR adds a read-only `_collect_memory_check()` slotted between the existing Knowledge Index and Skill Catalog checks.

## What the probe reports

```
[OK] Graph Memory: Memory database OK (schema=001_namespace, migrations=1, shared=61, kh_seeds=49)
  path=/home/.../.config/omicsclaw/memory.db
  size=806912 bytes
  schema_version=001_namespace
  migrations_applied=1
  shared_paths=61
  kh_seed_paths=49
```

| Condition | Status |
|---|---|
| DB exists, all required tables, KH seeds present | OK |
| `__shared__` populated but `kh_seed_paths == 0` (stale bootstrap) | WARN |
| Required tables missing (`nodes`/`memories`/`edges`/`paths`/`_schema_version`) | WARN |
| DB file not yet created | WARN |
| Directory missing / not writable / corrupt DB | FAIL |
| Non-SQLite backend (e.g. PostgreSQL) | INFO (file probe N/A) |

## Design notes

- **Side-effect-free.** Opens SQLite via `file:...?mode=ro` and reads `sqlite_master`, `_schema_version`, and `paths`. Does NOT call `init_db`, run migrations, or seed anything — doctor stays a pure diagnostic.
- **No new dependencies.** Uses the project's existing `sqlite3` stdlib path (same as `_collect_session_db_check`).
- **Credential safety.** Mirrors the password-redaction pattern from `omicsclaw/memory/database.py:152-159` (`_redact_memory_db_url`) so PostgreSQL URLs never echo credentials in doctor output. Local SQLite branches don't echo the URL at all — only the resolved file path, matching Session DB / Knowledge Index conventions.
- **Schema introspection helper** (`_probe_memory_schema` + private `_MemorySchemaProbe` dataclass) kept inline in `diagnostics.py` since this is the only caller today. Easy to lift to `omicsclaw/memory/health.py` if memory-server admin UI ever wants the same data.

## Test plan

- [x] `pytest tests/test_diagnostics.py` — **16 pass** (8 new)
  - `test_collect_memory_check_warns_when_db_not_yet_created`
  - `test_collect_memory_check_info_for_postgres_backend`
  - `test_collect_memory_check_redacts_password_in_postgres_url` *(regression guard for the URL-leak class)*
  - `test_collect_memory_check_reports_schema_version_when_initialized`
  - `test_collect_memory_check_reports_shared_and_kh_counts`
  - `test_collect_memory_check_warns_when_shared_lacks_kh_seeds`
  - `test_collect_memory_check_ok_for_empty_initialized_store`
  - `test_collect_memory_check_warns_when_required_tables_missing`
- [x] `pytest tests/memory/` — **253 pass** (no regressions)
- [x] `ruff check omicsclaw/diagnostics.py tests/test_diagnostics.py` — clean
- [x] Live `oc doctor` against the real working DB — `Overall: OK (fail=0, warn=0)`; new entry reports `schema=001_namespace, migrations=1, shared=61, kh_seeds=49` (matches independently-verified KH bootstrap of 49 seeds)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added a "Graph Memory" diagnostic to the doctor tool that validates database integrity, checks required schemas, and reports configuration status.

* **Tests**
  * Added comprehensive test coverage for the memory diagnostic feature, including validation scenarios and error cases.

<!-- review_stack_entry_start -->

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/197)

<!-- review_stack_entry_end -->

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d09979c5c6a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.