# Issue

**Title:** fix(memory): restore memory_store init + clarify disabled-store hint

## Description

## Summary

Two related fixes for the persistent-memory subsystem, each with a TDD-style regression test.

### 1. Restore `memory_store` initialization (root cause)

After commit `c5987a5` retired `omicsclaw.memory.graph.GraphService`, `bot/session.py` still imported it as a startup probe. The bare `except ImportError` arm in the memory-init block swallowed the resulting `ModuleNotFoundError` and logged the misleading **"Memory dependencies not installed"** warning, leaving `_core.memory_store=None` for every user who actually had the deps installed.

User-visible symptom: the interactive CLI's `remember` tool failed with *"Memory system not enabled"* even though `OMICSCLAW_MEMORY_ENABLED` defaulted to `true` and `OMICSCLAW_MEMORY_DB_URL` was set.

Fix: delete the stale import.

### 2. Replace bogus env-var name in the disabled-store hint

`execute_remember` / `execute_recall` / `execute_forget` returned

> `Memory system not enabled. Set OMICSCLAW_MEMORY_BACKEND=sqlite in .env`

when `bot.core.memory_store` was `None`. **That env var has never existed in the codebase** — the real switches are `OMICSCLAW_MEMORY_ENABLED` and `OMICSCLAW_MEMORY_DB_URL`, both documented under §"Graph Memory System" in `.env.example`. Users following the hint hit a dead end (`.env.example` has no such field).

Fix: extract a shared `_MEMORY_DISABLED_HINT` module constant that names the real env vars, references the log strings produced by the memory-init block (so users can grep their logs), and points at the existing `.env.example` section.

### Diff scope

| File | + / − | Purpose |
|---|---|---|
| `bot/session.py` | 1 / 2 | drop stale `omicsclaw.memory.graph` import |
| `bot/tool_executors.py` | 18 / 3 | shared actionable hint constant |
| `tests/test_bot_core_timeout.py` | 41 / 0 | regression: `init` populates `memory_store` when deps present |
| `tests/bot/test_tool_executors.py` | 45 / 0 | regression: 3 disabled-store hints name real env vars |

## Test plan

- [x] `pytest tests/bot/test_tool_executors.py tests/test_bot_core_timeout.py` — 25 passed
- [x] `pytest tests/bot/ tests/memory/ tests/test_bot_core_timeout.py` — 339 passed (wider regression sweep)
- [x] RED proven before GREEN for both fixes (failing test → fix → passing test)
- [x] Manual repro on interactive CLI: `remember` tool now succeeds against the user's real `.env`

## Follow-up (not in this PR)

The `except ImportError` arm at `bot/session.py:317` still logs *"Memory dependencies not installed"* without the actual exception — that's what let this bug hide. Worth a separate PR to include the exception message in the warning so the next stale import or missing dep is self-diagnosing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `726dacb3b3b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.