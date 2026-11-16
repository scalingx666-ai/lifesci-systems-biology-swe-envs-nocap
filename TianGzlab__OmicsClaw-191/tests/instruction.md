# Issue

**Title:** fix(oc-chat): surface actionable LLM-init diagnostics

## Description

## Summary

`oc chat` had two layers of confusing UX when no API key is configured:

1. `_init_llm` in `omicsclaw/interactive/interactive.py` caught `OpenAIError` but only emitted a `WARNING` to the logger — the CLI logger config drops that below the banner, so the user saw `Model: unknown` with no actionable hint at startup.
2. After the user sent their first message, `bot/agent_loop.py` returned `Error: LLM client not initialised. Call core.init() first.` — a private-API instruction the user cannot act on.

## What changed

Both surfaces now tell the user exactly what to do:

- `_init_llm` adds a yellow `console.print` warning under the banner that names `LLM_API_KEY` / `OPENAI_API_KEY` and points at `oc onboard`.
- `llm_tool_loop` returns the same actionable text when `_core.llm is None` instead of the cryptic developer message.

## Tests

TDD red→green; one focused test per behaviour:

- `tests/bot/test_agent_loop.py::test_llm_tool_loop_returns_actionable_message_when_llm_uninitialised` — pins the return text and explicitly forbids `Call core.init` reappearing.
- `tests/test_interactive_llm_init_diagnostics.py::test_init_llm_surfaces_actionable_message_when_core_init_fails` (new file) — monkeypatches `core.init` to raise `OpenAIError`, calls `_init_llm({})`, asserts the user-visible output contains the env-var name and `onboard` hint.

## Test plan

- [x] `pytest tests/bot/test_agent_loop.py tests/test_interactive_llm_init_diagnostics.py` → 14 passed
- [x] `pytest -k 'interactive or agent_loop'` (excluding pre-existing pydantic-v2 collection errors that also fail on `main`) → 144 passed, 10 skipped, 0 failed
- [x] Live smoke: deleted `LLM_API_KEY` env var, stubbed `core.init` to raise `OpenAIError`, called `_init_llm({})` — the yellow diagnostic prints to stdout
- [x] Live smoke: set `core.llm = None` and called `llm_tool_loop` — returns the actionable hint, no `Call core.init` text

## Before / after

Before:
```
Model: unknown
❯ hi
Error: LLM client not initialised. Call core.init() first.
```

After:
```
⚠ LLM init failed: Missing credentials. ...
Set LLM_API_KEY (or OPENAI_API_KEY) in your environment or .env file,
then restart `oc chat`. To configure interactively, run `oc onboard`.
Model: deepseek-v4-pro
❯ hi
⚠ LLM is not configured.
Set LLM_API_KEY (or OPENAI_API_KEY) in your environment or .env file,
then restart `oc chat`. To configure interactively, run `oc onboard`.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bb0341fc58bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.