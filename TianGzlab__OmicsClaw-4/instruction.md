# Issue

**Title:** docs: Enhance Feishu bot configuration with comprehensive setup guide

## Description

## Summary

Adds comprehensive bilingual documentation for Feishu bot setup, addressing the most common configuration pitfalls that prevent message reception.

## Changes

### Documentation
- **New**: `bot/FEISHU_SETUP.md` - Detailed step-by-step setup guide (Chinese + English)
  - Emphasizes the critical "publish version" step that 90% of users miss
  - Provides connection test workflow before full bot deployment
  - Lists exact permissions and event subscriptions needed

- **Updated**: `bot/README.md` - Simplified Feishu section to reference detailed guide

### Dependencies
- Added `httpx[socks]>=0.25.0` for proxy support in restricted network environments

### Testing Tools
- **New**: `run_longConnect.py` - Minimal WebSocket connection test script
  - Uses environment variables (secure, no hardcoded credentials)
  - Helps verify Feishu configuration before running full bot

### Configuration
- Fixed DeepSeek API URL example to include `/v1` path

## Why This Matters

The Feishu bot setup has a non-obvious requirement: **configuration changes don't take effect until you publish a new app version**. This causes most first-time users to get stuck with a bot that appears configured but doesn't receive messages. The new guide explicitly highlights this and provides a test-first workflow.

## Testing

Verified the connection test script successfully establishes WebSocket connection to Feishu's event service.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f5f14aaf072`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.