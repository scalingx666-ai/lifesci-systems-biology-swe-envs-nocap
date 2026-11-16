# Issue

**Title:** feat: Enhance spatial skills, fix domain detection, and bot improvements

## Description

## Summary

This PR includes environment fixes, spatial skill enhancements, and bot improvements.

## Changes

### Bug Fix
- Fix genomics, proteomics, and metabolomics domain detection in `dependency_manager.py` — these domains use only core dependencies and were incorrectly hardcoded as `False`

### Spatial Skills
- Improve `spatial-annotate`, `spatial-deconv`, `spatial-genes`, `spatial-preprocess` scripts with better error handling and robustness

### Bot Enhancements
- Add conversation memory system with SQLite persistence to bot core
- Improve Feishu and Telegram bot frontends (error handling, message formatting)
- Add `bot/data/` to `.gitignore` to prevent runtime database files from being tracked

### Dependencies & Config
- Update `pyproject.toml` and `.env.example`
- Update `omicsclaw.py` CLI and `omicsclaw/core/registry.py`

## Environment Status After This PR

All domain tiers and standalone layers show ✅ Installed (except BANKSY which requires numpy<2.0 in an isolated env).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `182f20fcbea9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.