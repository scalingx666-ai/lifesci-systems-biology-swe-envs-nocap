# Issue

**Title:** feat: Enhance Feishu bot group chat support and documentation

## Description

## Summary

Improves Feishu bot group chat functionality and clarifies critical permission requirements that cause 90% of group message reception issues.

## Changes

### Documentation (bot/FEISHU_SETUP.md)
- ⚠️ Highlight critical `im:message.group_msg` permission requirement
- Emphasize "Application Permission" type selection (not "User Permission")
- Add visual checklist with ✅/⚠️ indicators for all required permissions
- Improve troubleshooting guidance for group message reception issues
- Bilingual updates (Chinese + English)

### Code (bot/feishu_bot.py)
- Add group member count caching with 1-hour TTL
- Implement `_get_group_member_count()` function using Feishu Chat API
- Cache reduces API calls and improves performance
- Useful for future group-specific features (e.g., disable in large groups)

## Problem Solved

**Issue:** Users configure all visible permissions but still cannot receive group messages.

**Root Cause:** Missing `im:message.group_msg` permission, which is not obvious in the Feishu console.

**Solution:** Explicit documentation with visual emphasis on this critical permission.

## Testing

- Verified group member count API integration
- Confirmed caching mechanism works correctly
- Tested permission configuration flow with fresh Feishu app

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bc90fff91f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.