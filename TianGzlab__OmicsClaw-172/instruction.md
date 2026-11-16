# Issue

**Title:** feat(memory): seed core://kh/* into __shared__ on every surface startup

## Description

## TL;DR
Phase 1 of the memory-system migration closes the long-pending `core://kh/*` bootstrap. After this PR, every memory-init path on every surface seeds the knowledge handbook into `__shared__` on startup, so `recall("core://kh/<id>")` works from any namespace via the existing read-fallback. KH content remains the markdown corpus under `knowledge_base/knowhows/` — the bootstrap is a one-way mirror, not a takeover.

## Recommended review order

1. `omicsclaw/memory/engine.py` — `seed_shared` + `_ensure_shared_parent_chain` (the new primitive)
2. `omicsclaw/memory/bootstrap.py` — `seed_knowhows` (error containment + stats)
3. `omicsclaw/knowledge/knowhow.py` — `iter_entries` (URI shape decision)
4. Wiring sites (`compat.py`, `memory_client.py`, `app/server.py`, `memory/server.py`) — one-line additions
5. Tests — `test_seed_shared.py`, `test_kh_bootstrap.py`, `test_knowhow_iter_entries.py`

## Diff buckets

| Bucket | Files | Why |
|---|---|---|
| New primitive | `omicsclaw/memory/engine.py` | Idempotent shared write + parent auto-vivify |
| New bootstrap | `omicsclaw/memory/bootstrap.py` | Enumerate KH → seed each via `seed_shared` |
| New iterator | `omicsclaw/knowledge/knowhow.py` | Expose `(uri, content)` pairs |
| Surface wiring | 4 files | Call `seed_knowhows` right after `init_db()` |
| Coverage | 3 new test files (19 tests) | Idempotency, race-safety, wiring smoke, error containment |
| Docs | `README.md`, `AGENTS.md` | Reflect the new `__shared__` pool contents + retire stale migration note |

## Key design decisions

- **Bootstrap point: `init_db()` aftermath, called from each surface.** Not `oc onboard` (would force a UI step), not a standalone `oc seed` command (would split init responsibility). Each surface wires it once next to `init_db()` so the dependency is local and explicit.
- **Idempotency on content equality, not hash.** Bodies are a few KB each; string compare is cheap and avoids a parallel hash column.
- **Failures never block startup.** A missing `knowledge_base/` directory or per-entry error downgrades to a `logger.warning` and bumps a `failed` counter.
- **Race safety via PK + recovery probe.** Two concurrent surface boots could both pass the equality probe; the second hits `paths` PK violation, which we catch and resolve via a fresh recall. No data corruption (PK enforces uniqueness), no exception leaks (test pins this).

## Risk notes

- **`__shared__` partition now grows by ~50 rows on every fresh DB.** Existing query paths already read `__shared__`; the only behavior change is that those reads see KH content where previously they saw nothing. No surface depends on `__shared__` being empty.
- **`KnowHowInjector.read` unchanged.** RAG tool still reads from disk. A future PR can switch `read` to graph-read; this PR doesn't try to.
- **Container nodes get auto-vivified.** Seeding `core://kh/foo` first writes a `core://kh` parent with content `"Container node: core://kh"`. Matches the existing `MemoryClient._ensure_parent_chain` pattern. Visible to `list_children` / `search` — flagged in review as a potential future cleanup (could add `disclosure="internal"`).

## Verification

- 369 tests pass across memory/bot/app/integration on this branch.
- Concurrent stress: 10/10 runs of `test_seed_shared_concurrent_first_writes_do_not_corrupt` pass after the IntegrityError-recovery fix.
- Manual smoke (not required to repro): a fresh `oc app-server` startup writes `~50 core://kh/*` rows to `__shared__`; a second startup writes 0.
- 5-axis review run pre-push found one Important (TOCTOU race) which is fixed in commit fd200b9; remaining items are nits/hardening deferred as follow-up.

## Out of scope (follow-ups)

- `core://kh/*` read path migration — `read_knowhow` still hits filesystem.
- `doc_id` regex validation — current KH files are repo-controlled, threat model is low.
- Retiring `GraphService` from the three internal API modules (`omicsclaw/memory/api/{browse,maintenance,review}.py`) — Phase 2 of the migration plan.
- Centralised `bootstrap_memory_engine(...)` helper — the 4 wiring sites are still simple enough that the duplication isn't paying for itself yet.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Knowledge handbook entries are now automatically seeded into shared memory during application startup, ensuring core agent identity and reference materials are consistently available across surfaces.

* **Documentation**
  * Updated documentation to clarify the shared memory pool and its role in providing agent identity, reference materials, and shared context across all surfaces.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/172)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a84fc5b51789`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.