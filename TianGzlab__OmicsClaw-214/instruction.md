# Issue

**Title:** fix(providers): discover Ollama models live and tag tool capability

## Description

.

## Summary
- `/providers` now probes Ollama `/api/tags` (TTL-cached 30s) and merges discovered models into the registry payload, so the dropdown shows what the user actually pulled — not a stale curated list. Falls back to the curated list when the daemon is unreachable.
- Each ollama `model_metadata` entry carries `supports_tools: True/False/None` via a longest-prefix family classifier, so the frontend can disable tool-incapable picks before they fail.
- Curated list refreshed: `qwen3:8b`, `llama3.1:8b`, `gemma4:e4b`, `gemma4:26b` added. Gemma 4 (released 2026-04-02) ships native function calling per the [Ollama capabilities row](https://ollama.com/library/gemma4/tags) — distinct from gemma2/gemma3 which remain text-only.
- Runtime translates the upstream `does not support tools` 400 into actionable guidance pointing at known-capable models (`qwen2.5:7b`, `qwen3:8b`, `llama3.1:8b`, `llama3.3:70b`, `gemma4:e4b`, `mistral`, `command-r`).

## Why
The reporter had `gemma4` (a real, tool-capable model) installed locally but it never appeared in the OmicsClaw model picker — the picker was a static tuple in `PROVIDER_DISPLAY_METADATA`. They then fell back to `deepseek-r1:14b`, which Ollama rejects for tool calls; the raw 400 surfaced as `Sorry, I'm having trouble thinking right now -- API error: ...`. Both problems share the same root cause: nothing in the production path consulted Ollama for live capability, and nothing in the picker knew which families can hold a tool-using agent.

## Files
- `omicsclaw/providers/patches.py` — `model_supports_tools_ollama()` classifier (longest-prefix match over capable/incapable pattern lists, includes the 2026-04 Gemma 4 release).
- `omicsclaw/providers/registry.py` — `build_provider_registry_entries(..., discovered_models=...)` kwarg + curated list refresh + `supports_tools` on `ModelMetadata`.
- `omicsclaw/surfaces/desktop/server.py` — `_cached_ollama_models` helper wired into `GET /providers` with a 30s TTL.
- `omicsclaw/runtime/agent/loop.py` — friendlier error for the `does not support tools` 400.
- `tests/test_llm_patches.py` — 12 new cases covering family disambiguation (qwen2.5 vs qwen2, llama3.1 vs llama3, gemma4 vs gemma3, embedding models, unknown → None).

## Verification
Used a hermetic before/after probe (stash → run → pop → run) with `discover_ollama_models_async` stubbed:

| Surface | Baseline | Treatment |
|---|---|---|
| `/providers` ollama.models | 8 curated only | 12 curated + any discovered names prepended |
| `model_metadata.supports_tools` | field absent | `True`/`False` per family, `None` for unknown |
| Runtime error on `does not support tools` 400 | `Sorry, I'm having trouble thinking …` | `The selected Ollama model … pick … qwen2.5:7b, qwen3:8b, llama3.1:8b, llama3.3:70b, gemma4:e4b, mistral, or command-r …` |

Pattern classifier spot-check across the Gemma line:
| Model | supports_tools |
|---|---|
| `gemma2:9b`, `gemma3:4b`, `gemma3:12b` | `False` |
| `gemma3n:e4b` | `None` (unknown — passthrough) |
| `gemma4:e2b`/`e4b`/`26b`/`31b`/`latest` | `True` |

## Test plan
- [x] `pytest tests/test_llm_patches.py` — 29/29 pass.
- [x] Full provider-touching subset: 319 passing (baseline was 307); 6 pre-existing unrelated failures unchanged.
- [x] Smoke imports for desktop server / providers / runtime modules.
- [ ] Manual UI verification with an Ollama daemon running locally — out of scope for this remote test box.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Local Ollama models are now auto-discovered and shown in the provider/model list.
  * Models are classified for tool-calling capability to surface compatibility hints.
  * Error messages now offer guidance when a selected model doesn’t support tools.

* **Tests**
  * Added tests for model tool-capability classification and Ollama discovery/URL normalization/cache behavior.

<!-- review_stack_entry_start -->

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/214?utm_source=github_walkthrough&utm_medium=github&utm_campaign=change_stack)

<!-- review_stack_entry_end -->
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e39c378ab17`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.