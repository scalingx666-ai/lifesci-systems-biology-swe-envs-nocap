# Issue

**Title:** fix(providers): make /providers/test tolerate reasoning-model outputs

## Description

## Problem

OmicsClaw Desktop App's settings → connection diagnostic always returns

> Live provider test returned an empty response.

whenever the active provider is **`deepseek-v4-flash`** or **`deepseek-v4-pro`**, even with valid credentials and a reachable endpoint. The user can chat normally, but the diagnostic falsely reports a failure.

## Root cause

`omicsclaw/app/server.py::test_provider` issued the smallest possible probe — `messages=[{"Say OK"}], max_tokens=8` — and judged success solely by whether `message.content` came back non-empty.

Two assumptions break for the DeepSeek V4 series:

1. **The visible answer is on `message.content`.** V4-flash / V4-pro are thinking-mode endpoints; the chain-of-thought output is on a non-standard **`message.reasoning_content`** field. The codebase already documents this quirk in `omicsclaw/core/llm_patches.py` ("DeepSeek V3.x/V4 thinking-mode endpoints…").
2. **8 tokens is enough.** V4 burns the entire budget on internal reasoning and emits `finish_reason="length"` before any visible content can land in either channel.

So the API call succeeds, credentials and routing are verified, but the test reports "empty response" because the success criterion was too narrow.

## Fix

Treat `/providers/test` as a **connectivity probe**, not a literal-text validator.

| Change | Reason |
|---|---|
| `max_tokens` 8 → 64 | Reasoning models keep room for a visible final answer after thinking |
| Accept `content` **or** `reasoning_content` **or** `tool_calls` as a pass signal | All three are legitimate "the model responded" shapes (V4, R1, function-calling models) |
| On failure, append `finish_reason` to the message | Lets users distinguish `length` (raise max_tokens), `content_filter` (provider blocked the prompt), and `stop` (model genuinely returned nothing) |
| On success, return a `detail` field listing which signals hit | Surfaces diagnostic context in the App's doctor panel (e.g. `"reasoning_content, finish_reason=length"`) |

All extractions use `getattr(..., default)` so providers without `reasoning_content` (OpenAI, Anthropic-via-proxy, etc.) just see `""` and fall back to `content` — no behavior change on the OpenAI happy path.

## Verification

```
$ pytest tests/test_app_server.py -k provider_test
3 passed in 2.87s
```

| Test | What it locks down |
|---|---|
| `test_provider_test_closes_async_openai_client` *(existing)* | OpenAI-shape happy path + resource cleanup — unchanged contract |
| `test_provider_test_accepts_reasoning_only_response` *(new)* | V4 thinking shape: `content=""`, `reasoning_content` populated, `finish_reason="length"` → **PASSED** with `detail` listing the signal |
| `test_provider_test_empty_response_includes_finish_reason` *(new)* | Truly-empty path → **FAILED** with `finish_reason=content_filter` surfaced in the message |

## Risk / Compatibility

- **API-shape additive only**: success payload gains a `detail` field; existing consumers ignoring unknown fields are unaffected.
- **Non-DeepSeek providers**: `getattr(message, "reasoning_content", "")` returns `""` when the attribute doesn't exist, so the OpenAI / Anthropic-compatible path keeps using `content` exactly as before.
- **Companion Desktop App work**: the new `detail` field flows through the existing `src/app/api/providers/doctor/route.ts` handler in OmicsClaw-App with no app-side change required.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **Bug Fixes**
  * Enhanced OpenAI-compatible provider response handling to properly recognize and process responses containing content, reasoning signals, and tool calls
  * Improved error diagnostics with detailed feedback on detected response components for better troubleshooting

* **Tests**
  * Added test coverage for reasoning-only response scenarios and empty response handling

<!-- review_stack_entry_start -->

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/205)

<!-- review_stack_entry_end -->

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7baf56184ec8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.