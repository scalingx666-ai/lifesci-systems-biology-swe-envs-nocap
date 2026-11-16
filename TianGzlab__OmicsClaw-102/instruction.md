# Issue

**Title:** fix(runner): live log streaming, cancel-kills-subprocess, registry alias shadow

## Description

## TL;DR

Closes the three runtime guardrails deferred from PR #101's review: bot operator console no longer goes silent during long deep-learning skills, cancelled jobs actually kill the subprocess, and registry alias views can no longer corrupt each other through shared dict mutation.

Built incrementally with TDD red-green; each increment is its own commit with a focused test that fails before the change and passes after.

## What changed

### W5 — registry alias dict shadow (`e01244d`)
Each alias key (canonical, legacy aliases, directory-name fallback, hardcoded post-block) now gets its own `copy.deepcopy` of the skill info dict. Previously every alias pointed at the same object; mutating one view (e.g. `info["allowed_extra_flags"].add(...)`) silently propagated to every other view. Read-only today, but a foot-gun for future callers. Cost is negligible — registry loads once over ~89 skills.

Test: assert top-level replacement and in-place set mutation under one alias do not leak to a sibling alias.

### W1 — stdout/stderr streaming (`9816887`, `e68cbbe`)
`run_skill` now accepts `stdout_callback` / `stderr_callback`. Replaces the single `popen.communicate()` blocking call with two daemon threads that drain each pipe via `readline()`, accumulate into the same aggregated `stdout`/`stderr` strings (return-value contract unchanged), and forward each line (newline stripped) to the callback. Callback exceptions are swallowed so a buggy log handler cannot abort an analysis. Default `callback=None` keeps prior behavior bit-for-bit.

The bot's `_run_skill_via_shared_runner` adapter now passes callbacks that emit each line to `omicsclaw.bot` logger with `[<canonical>:stdout]` / `[<canonical>:stderr]` prefixes — restoring the live operator console behavior we had before the runner refactor.

Tests:
- Real-subprocess: a fake skill prints 3 stdout lines and 1 stderr line; assert callback receives them in order without trailing newlines, and aggregated fields are unchanged.
- Robustness: a callback that raises must not break the run.
- Bot wiring: with `caplog`, the bot logger receives every streamed line.
- Existing `test_output_ux` `FakePopen` updated to expose `.stdout` / `.stderr` streams (the contract changed from `communicate()` to per-pipe `readline()`).

### W2 — cancel kills subprocess (`f03b0a4`, `d6357aa`)
`run_skill` now accepts an optional `cancel_event: threading.Event`. A watcher thread polls the event; when set it sends `SIGTERM` to the child's process group, waits up to 5 seconds for clean shutdown, and escalates to `SIGKILL` if the child is still alive. Uses the existing `start_new_session=True` group isolation so we never touch the parent.

`SkillRunnerExecutor.run` creates the event, forwards it to `run_skill`, and on `asyncio.CancelledError` sets the event before re-raising — so a cancelled FastAPI `/jobs` task actually terminates the underlying subprocess instead of leaking it.

Tests:
- A fake skill that would naturally run for ~30s is cancelled after 1 second; `run_skill` returns within 10s with `success=False` and non-zero exit code.
- The executor's asyncio task is cancelled while a fake `run_skill` blocks on the event; assert the captured event is set after cancel propagates.

## Verification

```bash
conda run -n OmicsClaw python -m pytest <18-test list from PR #101> -q
```
→ **192 passed** (was 186; +6 new tests across the three guardrails).

## Risk notes

- Default callback / cancel_event are `None`, preserving existing behavior for every caller that doesn't opt in. The signature change is forward-compatible.
- The streaming refactor did require updating `FakePopen` mocks in `test_output_ux.py` to expose `.stdout` / `.stderr` streams; this is the only test contract change.
- SIGKILL escalates after 5s grace. If a skill genuinely needs longer cleanup, the grace can be made configurable in a follow-up — for now 5s matches the prior `_reaper`'s implicit 0.5s + cleanup pattern.

## Out of scope

W4 (multi-input contract propagation to bot/agents/interactive) is deferred to a separate PR — it requires changes to chat parsing and tool spec definitions that don't share a logical unit with these runtime guardrails.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Implemented real-time streaming of skill execution logs with structured formatting
  * Added graceful cancellation support for running skills with automatic timeout escalation

* **Improvements**
  * Enhanced skill metadata handling for better data isolation across registry aliases

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae43724c3b28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.