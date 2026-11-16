# Issue

**Title:** feat(interactive): wire CLI/TUI /memory to the graph engine

## Description

## Summary

- `/memory remember|recall|search` now route through `MemoryClient` bound to `cli_namespace_from_workspace(workspace_dir)`; ScopedMemory keeps the `scope/list/add/prune` subcommands for markdown notes
- TUI dispatches graph subcommands via `run_worker` to mirror `/doctor` and `/context`
- Resolves the deferred CLI/TUI binding flagged in `docs/CONTEXT.md` and satisfies refactor-plan Task 5.1
- Open question on `~/` namespace resolved: `cli_namespace_from_workspace(None)` returns the resolved cwd

## Why

CLI/TUI was the only wired surface without graph memory — users running `oc interactive` had no way to write/read cross-surface knowledge that Desktop and the bots already use. The infrastructure (`get_memory_client`, `cli_namespace_from_workspace`) has been in place since PR #4a; this PR is the surface-side wiring.

## Test plan

- [x] `pytest tests/memory/test_cli_graph_memory_command.py` — 7 new cases (round-trip, cross-workspace isolation, FTS hit, URI validation, missing-arg usage, help-text)
- [x] `pytest tests/memory/ tests/test_interactive_memory_command_support.py tests/test_scoped_memory.py tests/test_interactive_loop.py tests/test_context_assembler.py` — 281 passed
- [x] Manual: `/memory remember dataset://pbmc.h5ad "10x PBMC"` → `/memory recall dataset://pbmc.h5ad` round-trips and echoes the workspace namespace

## Files

| File | Change |
|---|---|
| `omicsclaw/interactive/_memory_command_support.py` | +`build_graph_memory_command_view` (async), `is_graph_memory_subcommand`, `GRAPH_MEMORY_SUBCOMMANDS`; help-text update |
| `omicsclaw/interactive/interactive.py` | `_handle_memory` pre-dispatches graph subcommands |
| `omicsclaw/interactive/tui.py` | `/memory` branch pre-dispatches; new `_run_graph_memory_async` worker |
| `tests/memory/test_cli_graph_memory_command.py` | 7 new tests |
| `docs/CONTEXT.md` | Surface table marks CLI/TUI wired |
| `docs/2026-05-09-memory-refactor-plan.md` | Task 5.1 acceptance checked off; `~/` question resolved |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4b9cc23b5a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.