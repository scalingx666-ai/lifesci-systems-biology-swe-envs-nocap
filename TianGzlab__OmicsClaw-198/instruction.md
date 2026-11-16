# Issue

**Title:** fix(app): surface preflight needs_user_input on desktop chat

## Description

## Summary

Desktop chat silently swallowed preflight confirmation prompts. When a skill emitted `USER_GUIDANCE_JSON: {... "status": "needs_user_input"}` and exited non-zero (by design — `decision.raise_if_blocking()`), the desktop frontend received `is_error=True` on the `tool_result` event and collapsed it into an error tile. The user had no way to see — let alone confirm — the prompt.

Reproduced by running `sc-preprocessing` on `pbmc3k_raw.h5ad` without first running `sc-qc`: preflight wants "confirm default thresholds are OK", but the question never surfaces in the desktop chat.

## Root cause

```
sc-preprocessing subprocess
    ↓ emits USER_GUIDANCE_JSON: needs_user_input
    ↓ decision.raise_if_blocking() → exit non-zero
bot.agent_loop._build_tool_result_callback_metadata
    ↓ success=False → is_error=True            ← the trap
omicsclaw/app/server.py on_tool_result
    ↓ metadata.is_error=True → frontend collapses tool_result as error tile
user sees: silent failure, no prompt
```

The bot path's existing `bot.preflight` state machine DOES stash the pending request and CAN auto-resume when the user replies "yes" — but only if the user ever sees the confirmation in the first place. On the desktop the prompt was hidden.

## Fix

Three-slice change:

1. **`bot/agent_loop.py`** — `_build_tool_result_callback_metadata` accepts a kw-only `pending_preflight: dict | None`. When set (and not also a real timeout — those must not be masked), it demotes `is_error=False` and tags `preflight_pending=True` + the original payload.
2. **`bot/agent_loop.py`** — `after_tool` passes the already-extracted preflight payload (same condition that already triggers `_remember_pending_preflight_request`) through to the metadata builder.
3. **`omicsclaw/app/server.py`** — `on_tool_result` reads `metadata.preflight_pending` and emits a dedicated `preflight_pending` SSE event with `{session_id, tool_use_id, tool_name, payload}` after the existing `tool_result` event.

The resume path in `bot.preflight._maybe_resume_pending_preflight_request` is unchanged — when the user replies affirmatively on their next turn, the omicsclaw tool call is re-issued with `confirmed_preflight=True` and the skill proceeds.

## Behaviour matrix

| success | timeout | preflight payload | is_error | preflight_pending |
|---|---|---|---|---|
| True | F | — | False | (unset) |
| False | F | None | True | (unset) |
| False | F | dict | **False** | True |
| False | T | dict | **True** | True (marker preserved, but timeout wins) |

A real timeout still classifies as an error — preflight cannot mask a hung run.

## Effect

**Before:** skill emits `needs_user_input` → exits non-zero → `is_error=True` → frontend hides the tool_result → user sees a silent failure with no way to proceed.

**After:** skill emits `needs_user_input` → exits non-zero → `is_error=False`, `preflight_pending=True` → frontend renders the guidance content AND receives a structured `preflight_pending` SSE event it can use to light up a confirmation modal → user replies "yes" → `bot.preflight` resumes with `--confirmed-preflight` → skill completes.

Telegram/Feishu channels are unaffected: they receive the new metadata key but ignore it. Their existing rendering of the `guidance_block` text continues to work, and is no longer hidden behind an error tile.

## Test plan

- [x] `pytest tests/bot/ tests/test_app_server.py` — **143 pass** (6 new)
  - `test_build_tool_result_callback_metadata_marks_failure_as_error` *(baseline)*
  - `test_build_tool_result_callback_metadata_demotes_preflight_pending_from_error`
  - `test_build_tool_result_callback_metadata_timeout_overrides_preflight_demotion`
  - `test_after_tool_forwards_pending_preflight_payload_to_on_tool_result`
  - `test_after_tool_does_not_mark_preflight_pending_for_normal_failure` *(counter-example)*
  - `test_chat_stream_emits_preflight_pending_event_for_omicsclaw_tool` *(E2E SSE)*
- [x] Manual reproduction: `sc-preprocessing --input pbmc3k_raw.h5ad --confirmed-preflight` runs end-to-end (2699 cells × 2000 HVGs, processed.h5ad written). Without the flag, preflight still blocks as designed. This PR is about surfacing the prompt, not changing the policy.

## Follow-ups (out of scope)

- **Frontend (TypeScript)**: subscribe to the new `preflight_pending` SSE event to render a dedicated confirmation modal (Yes / Run sc-qc first). Even without this, this PR is an immediate win: the guidance content is no longer hidden as an error, so the user can read the LLM's transcription and reply "yes" inline to trigger the resume path.
- **Bot channels**: Telegram/Feishu could read `metadata.preflight_pending` to surface inline buttons. Not required for the fix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0979ccfa11a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.