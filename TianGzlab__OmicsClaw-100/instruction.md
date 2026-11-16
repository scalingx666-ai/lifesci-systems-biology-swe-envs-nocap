# Issue

**Title:** Fix custom provider runtime diagnostics

## Description

## TL;DR
Hardens Custom Endpoint runtime handling across both surfaces:

- OmicsClaw-App backend provider switching / diagnostics no longer drift from the selected Custom Endpoint runtime.
- `oc chat` now honors the backend `.env` Custom Endpoint config and reports actionable endpoint diagnostics instead of `(no response)`.

## Root Cause
There were two related failures:

1. App/backend chat runtime could keep stale provider state when only the model changed or when Custom Endpoint needed the saved Base URL.
2. CLI `core.init()` without explicit args did not consume generic Custom Endpoint env (`LLM_BASE_URL`, `OMICSCLAW_MODEL`, `LLM_API_KEY`), so `oc chat` could fall back to OpenAI defaults or mask malformed endpoint responses as `(no response)`.

While reproducing the reported CLI issue, the current `.env` used `LLM_BASE_URL=https://api.biom.autos`. That URL returns the provider dashboard HTML at `/chat/completions`; `https://api.biom.autos/v1` is the OpenAI-compatible API root and returns a valid chat completion.

## What Changed
- `/chat/stream` reinitializes provider runtime when a request changes model on the same provider id.
- Custom Endpoint switches are rejected unless model and Base URL are resolvable.
- Chat-initiated Custom Endpoint reinitialization preserves saved `LLM_BASE_URL` / `OMICSCLAW_BASE_URL`.
- `/providers` reflects the active Custom Endpoint model and Base URL back to desktop clients.
- Added `POST /providers/test` for short live provider connectivity probes.
- `resolve_provider()` now honors generic Custom Endpoint env only when it belongs to the active/requested provider, avoiding stale `LLM_BASE_URL` leakage into explicit provider switches.
- `oc chat` single-shot and interactive initialization now pass explicit `--provider` / `--model` overrides into `core.init()`.
- Empty LLM completions now return a provider diagnostic that points users at OpenAI-compatible base URL requirements, commonly `/v1`.
- Graph memory imports are lazy enough for lightweight chat installs; missing graph-memory deps no longer block importing interactive CLI or repeatedly pollute chat output.

## Suggested Review Order
1. App server provider/runtime helpers in `omicsclaw/app/server.py` and tests in `tests/test_app_server.py`.
2. Provider resolution changes in `omicsclaw/core/provider_registry.py`.
3. CLI initialization changes in `omicsclaw/interactive/interactive.py`.
4. Runtime empty-completion and LLM error messaging in `omicsclaw/runtime/query_engine.py` and `bot/core.py`.
5. Lazy memory package import in `omicsclaw/memory/__init__.py`.
6. Regression tests in `tests/test_provider_registry.py`, `tests/test_bot_core_timeout.py`, `tests/test_interactive_loop.py`, and `tests/test_query_engine.py`.

## Cross-Repo Dependency
Companion OmicsClaw-App PR:
-

The App PR consumes `/providers/test` for live Provider Doctor logs and relies on `/providers` reflecting the active custom model/Base URL.

## Verification
- `pytest -q tests/test_provider_registry.py tests/test_bot_core_timeout.py tests/test_interactive_loop.py tests/test_query_engine.py tests/test_runtime_env.py` (62 passed, 2 skipped)
- `python -m py_compile bot/core.py omicsclaw/core/provider_registry.py omicsclaw/runtime/query_engine.py omicsclaw/memory/__init__.py omicsclaw/interactive/interactive.py`
- `git diff --check`
- `ALL_PROXY= all_proxy= LLM_BASE_URL=https://api.biom.autos/v1 timeout 90 python omicsclaw.py chat -p "Say exactly OK."` -> `OK`
- `ALL_PROXY= all_proxy= timeout 60 python omicsclaw.py chat -p "Say exactly OK."` with current `.env` `https://api.biom.autos` -> actionable Custom Endpoint diagnostic, not `(no response)`
- Earlier app-server targeted checks: `python -m pytest tests/test_app_server.py::test_chat_stream_reapplies_provider_when_model_changes tests/test_app_server.py::test_switch_provider_rejects_incomplete_custom_endpoint tests/test_app_server.py::test_list_providers_reflects_active_custom_endpoint -q` (3 passed, 1 Jupyter path warning)

## Risk Notes
- `/providers/test` performs a minimal OpenAI-compatible chat completion (`Say OK`) against the configured runtime. Failures are returned as structured diagnostic payloads rather than raised as 5xx after the provider request starts.
- Generic `LLM_BASE_URL` / `LLM_API_KEY` are intentionally applied only when the selected provider matches the configured env provider, so stale Custom Endpoint config does not contaminate explicit OpenAI/DeepSeek/etc switches.
- For the reported backend CLI environment, set `LLM_BASE_URL=https://api.biom.autos/v1` to use the actual OpenAI-compatible API endpoint.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Live provider testing endpoint to validate provider configurations.
  * CLI/provider runtime resolution improvements for interactive CLI overrides and diagnostics.

* **Improvements**
  * Richer provider metadata (active state, default model) and deterministic environment persistence after switches.
  * Cleaner, provider-aware LLM error messages with actionable hints.
  * Clearer messaging for empty LLM completions.
  * Unified CLI logging behavior to reduce noisy output.

* **Documentation**
  * README expanded with desktop provider and CLI/runtime guidance.

* **Tests**
  * Added tests covering provider resolution, provider-switch behavior, interactive init, and empty-completion handling.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fb79d6e6230`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.