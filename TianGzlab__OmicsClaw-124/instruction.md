# Issue

**Title:** refactor(bot): extract bot/agent_loop.py — final bot/core.py collapse to 661 LOC (PR-B)

## Description

## Summary

PR-B — final slice of the bot/core decomposition. Carves the multi-round LLM dispatch loop (`llm_tool_loop`) and its helpers out of `bot/core.py` into `bot/agent_loop.py`. .

**`bot/core.py` is now 661 LOC (−87.2% from the 5160 baseline on main pre-PR #122).**

> **Branch base**: this PR is stacked on top of PR #123 (`refactor/bot-core-decomposition-followup`) — merge #123 first, then this one.

Refs PRD #113, ADR 0001 (local), milestone "bot/core decomposition".

## What ships

| | |
|---|---|
| New module | `bot/agent_loop.py` (908 LOC) |
| Re-exports (lazy) | 18 names: `llm_tool_loop`, `SYSTEM_PROMPT`, `MAX_TOOL_ITERATIONS`, `get_tools`, `get_tool_registry`, `_build_*`, `_format_llm_api_error_message`, callback adapters, timeout extractors, preflight resume |
| New tests | `tests/bot/test_agent_loop.py` — 6 cases |
| `bot/core.py` | 1441 → 661 LOC (−780) |

### The lazy re-export pattern (architectural change)

To avoid a circular load when `bot.agent_loop` is imported before `bot.core`, the agent-loop names are **not eagerly re-exported in `bot.core`**. Instead, `bot.core.__getattr__` lazily resolves them via `import bot.agent_loop` on first access. The 18-name set is enumerated in `_AGENT_LOOP_REEXPORTS` at the top of `__getattr__`. External callers reading `bot.core.llm_tool_loop` or `bot.core.SYSTEM_PROMPT` continue to work unchanged because Python falls through to `__getattr__` when the name isn't in module globals.

### Behavior tests added (6)

* **Tracer**: `llm_tool_loop` lives at canonical `bot.agent_loop` and is a coroutine.
* **Identity**: `bot.core.llm_tool_loop is bot.agent_loop.llm_tool_loop` (lazy re-export resolves to same object).
* **Production callers contract**: `llm_tool_loop` accepts every kwarg that `omicsclaw/app/server.py:1740` and `omicsclaw/interactive/interactive.py:1505` pass.
* **Pure helpers**: `_coerce_timeout_seconds` / `_extract_timeout_seconds_from_text` / `_format_llm_api_error_message`.

### Deferred — heavy integration tests

The PRD #121 acceptance criteria mentions full fake-LLM-client integration tests (single-round / multi-round / streaming / error paths). Those require substantial fixture scaffolding for a 25-kwarg coroutine and were deferred — the existing T9 behavioural-parity suite (`tests/eval/` against `deepseek-v4-pro`, 14/15 baseline) covers the contract end-to-end. Tracked as a future follow-up. This PR ships the extraction safely on top of that net.

## Verification

- [x] `pytest tests/bot/test_agent_loop.py`: **6 / 6 pass**
- [x] Bot regression net (`tests/test_bot_*`, `tests/test_oauth_regressions.py`, `tests/test_app_server.py`, `tests/test_notebook_files.py`, `tests/test_routing_regression.py`, `tests/test_auto_routing_disambiguation.py`, `tests/test_skill_listing.py`, `tests/test_bot_core_timeout.py`, `tests/bot/`, `tests/runtime/preflight/`): **234 passed, 1 skipped, 4 xfailed** — no regressions.
- [x] `pytest tests/eval/ tests/test_knowhow.py`: **121 passed, 17 deselected**. Eval baseline 14/15 against `deepseek-v4-pro` unaffected.
- [x] `python -c "import bot.agent_loop; import bot.core; assert bot.core.llm_tool_loop is bot.agent_loop.llm_tool_loop"` — lazy re-export verified.

## Cumulative decomposition outcome

After this PR + #122 + #123 land on main:

```
bot/core.py:               5160 → 661 LOC  (−87.2%)
bot/billing.py:                     151 LOC  (PR #122)
bot/audit.py:                        61 LOC  (PR #122)
bot/rate_limit.py:                   38 LOC  (PR #122)
bot/path_validation.py:             168 LOC  (PR #122)
bot/session.py:                     335 LOC  (PR #122)
bot/preflight.py:                   280 LOC  (PR #122)
bot/skill_orchestration.py:         771 LOC  (PR #122 + #123)
bot/tool_executors.py:             1900 LOC  (PR #123)
bot/agent_loop.py:                  908 LOC  (this PR)
omicsclaw/runtime/preflight/sc_batch.py:  440 LOC  (PR #122)
```

Each new module has a focused responsibility documented in its docstring and ADR 0001. `bot/core.py` is now a thin facade owning only path constants, init-mutable globals (`llm`, `OMICSCLAW_MODEL`, ...), the lazy `__getattr__` resolver, and a few text utilities.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Introduced multi-round LLM-powered tool dispatch system with intelligent context management and error handling.
  * Added slash commands for session management (`/clear`, `/new`, `/forget`, `/plan`, `/compact`) and information retrieval (`/files`, `/outputs`, `/skills`, `/status`, `/version`, `/help`, etc.).
  * Expanded tool capabilities: skill execution, file operations, audio generation, literature parsing, GEO metadata fetching, and custom analysis workflows.

* **Tests**
  * Added comprehensive test coverage for agent loop and tool execution contracts.

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/124)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e4dc05fc69d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.