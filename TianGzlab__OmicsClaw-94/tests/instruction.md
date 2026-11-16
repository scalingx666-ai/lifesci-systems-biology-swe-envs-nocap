# Issue

**Title:** feat(providers): refresh DashScope preset to Qwen3 / Qwen3.6 SKUs

## Description

## Summary

Default switches from `qwen-max` to `qwen3-max` (flagship, supports thinking). Adds `qwen3.6-plus` so OmicsClaw-App users can access Alibaba's latest Plus tier directly via the standard DashScope OpenAI-compatible endpoint — no need for a separate Bailian Coding Plan entry, which would only duplicate UX.

Model list now covers the six scenarios people actually pick: `qwen3-max`, `qwen3.6-plus`, `qwen3-coder-plus`, `qwq-plus`, `qwen3.5-flash`, `qwen-turbo-latest`.

Drops `qwen3-235b-a22b` (open-weight name, not an API SKU) and the `qwen-max` / `qwen-*-latest` legacy aliases — those track Qwen2 snapshots, not Qwen3, and keeping them in the dropdown would point users at the older generation.

## Test plan

- [ ] `pytest tests/test_provider_registry.py`
- [ ] Manual: select DashScope provider in OmicsClaw-App, verify the model dropdown lists the six new SKUs and `qwen3-max` is default.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd4ad5f1f375`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.