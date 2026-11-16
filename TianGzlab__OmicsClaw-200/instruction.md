# Issue

**Title:** fix(memory): break "记住" ambiguity that routed remember requests to task_create

## Description

## Summary

Sessions trace on the desktop surface shows the LLM frequently picks `task_create` when the user says `"记住 X"` / `"remember X"` — saving the user's preference as an engineering todo (e.g. session `945434f1`: `"记住我需要你用中文回答"` became a task titled `"用户语言偏好：中文回答"` saved under `engineering_tasks/`, never reaching `memory.db`). The user sees a green "success" event from the wrong tool and the Memory page stays empty.

## Defense in depth

1. **`memory_hygiene_rule`** (system prompt, gated by the memory-keyword predicate) now names `task_create` explicitly as the wrong tool, tying the disambiguation to the rule the LLM already sees when the trigger fires. Rule still under the 400-char budget.
2. **`remember` description** tells the LLM "Call this (not `task_create`) for '记住 X' / 'remember X' requests".
3. **`task_create` description** tells the LLM "Not for '记住 X' / 'remember X' — use `remember` for those".

Adds a regression test asserting the rule names `task_create` explicitly; the prior content assertions still pass. Snapshot fixtures regenerated.

## Test plan
- [x] `pytest tests/test_predicate_gated_injectors.py` — 16/16 pass (incl. new `test_memory_hygiene_rule_disambiguates_task_create`)
- [x] `pytest tests/test_tool_list_snapshots.py` — 14/14 snapshot tests pass; regenerated fixtures included
- [x] Manual reproduction on the failing session pattern (verified via sessions.db transcript)

## Note on pre-existing failure
`test_realistic_scde_tool_list_under_phase2_budget` reports 12662 chars vs 12500 budget. This failure pre-dates this commit (the sc-de scenario triggers many file-path tools that together blow the budget; `remember`/`task_create` are not in that selected set, so this PR does not move that number). Tracked separately.

## Pairing
Pairs with frontend commit on https://github.com/zhou-1314/OmicsClaw-App (`fix(memory): auto-refresh Memory page when chat tools mutate memory.db`) which adds a `refresh-memory` window event so the Memory page re-fetches after a successful `remember`/`forget` tool call.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `acc785950c7f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.