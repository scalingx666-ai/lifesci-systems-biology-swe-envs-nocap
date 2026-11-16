# Issue

**Title:** refactor: enhance knowledge system and bot tool handling

## Description

## Summary

This PR refactors the knowledge system and bot tool handling for improved routing accuracy and maintainability.

## Changes

**Knowledge system** (+153 lines):
- Refactor `omicsclaw/knowledge/knowhow.py` with improved query matching and routing logic
- Enhance `omicsclaw/knowledge/registry.py` with better indexing and retrieval mechanisms
- Add comprehensive test coverage in `tests/test_knowhow.py` (+119 lines)
- Add new `tests/test_knowledge_registry.py` for registry validation (+59 lines)

**Bot improvements**:
- Refactor `bot/core.py` with cleaner tool execution flow and error handling
- Update `bot/tests/test_tools.py` with additional test cases

## Benefits

- **Better routing accuracy**: Improved query matching in knowhow system
- **More robust**: Enhanced error handling in bot tool execution
- **Better tested**: Comprehensive test coverage for knowledge components
- **More maintainable**: Cleaner code structure and separation of concerns

## Test plan

- [ ] Run knowledge system tests: `pytest tests/test_knowhow.py tests/test_knowledge_registry.py -v`
- [ ] Run bot tests: `pytest bot/tests/test_tools.py -v`
- [ ] Test knowledge routing: verify skill recommendations are accurate
- [ ] Run full test suite: `pytest tests/`

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b4ca5746ed6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.