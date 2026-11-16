# Issue

**Title:** Fix DeepSeek V4 Pro TUI tool traces

## Description

## Summary
- Fix Textual TUI tool-trace rendering by mounting the Collapsible parent before its child container.
- Keep `omicsclaw.interactive` package import dependency-light via lazy `run_interactive` import.
- Enable adaptive thinking for gateway DeepSeek V4 models such as `deepseek/deepseek-v4-pro`.
- Add focused regression coverage for TUI mount order and DeepSeek V4 Pro gateway thinking.

## Review
- Critical: none found.
- Warning: no full Textual end-to-end launch in this environment because `textual` is optional/not installed here; behavior is covered with a minimal lifecycle regression test.
- Note: pytest emits an unrelated `jupyter_client` deprecation warning.

## Tests
- `python -m pytest tests/test_interactive_tui_support.py tests/test_app_server.py::test_build_thinking_extra_body_explicit_enabled_and_disabled tests/test_app_server.py::test_build_thinking_extra_body_adaptive_per_provider tests/test_app_server.py::test_build_thinking_extra_body_invalid_inputs tests/test_app_server.py::test_chat_stream_enables_adaptive_thinking_for_deepseek tests/test_provider_registry.py tests/test_llm_models.py tests/test_bot_core_token_prices.py tests/test_autoagent_llm_client_deepseek.py tests/test_query_engine_deepseek_passback.py tests/test_query_engine_reasoning_capture.py -q`
  - Result: 143 passed, 1 unrelated warning
- `python -m py_compile omicsclaw/interactive/__init__.py omicsclaw/interactive/_tui_support.py omicsclaw/interactive/tui.py omicsclaw/app/server.py`
  - Result: passed
- `git diff --check`
  - Result: passed

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added support for "deepseek-v4" model with extended thinking capabilities.

* **Documentation**
  * Updated developer notes describing TUI helper dependency management and widget mounting best practices.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b05a45f603a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.