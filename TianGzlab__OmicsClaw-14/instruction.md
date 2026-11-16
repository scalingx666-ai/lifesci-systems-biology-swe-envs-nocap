# Issue

**Title:** feat: Enhance bot capabilities and spatial domain analysis

## Description

## Summary

This PR enhances OmicsClaw with improved bot functionality and spatial domain analysis capabilities.

## Key Changes

### Bot Enhancements
- Add conversation memory system with SQLite persistence for context retention
- Improve Feishu bot error handling and message formatting
- Add bot/data/ directory for persistent storage

### Spatial Domain Analysis
- Enhance spatial domain identification with multiple clustering methods (Leiden, Louvain, KMeans)
- Add comprehensive methodology documentation to SKILL.md
- Improve spatial_domains.py with better parameter handling

### Dependencies
- Update pyproject.toml with required bot dependencies
- Add memory and conversation management libraries

## Testing

All changes have been tested locally with demo data.

## Related Issues

Continues improvements from recent PRs #13, #12, #11, #9, #8, #7, #6, #4

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `045cd4e810df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.