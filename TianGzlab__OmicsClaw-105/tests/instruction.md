# Issue

**Title:** refactor(interactive): replace state dict with typed SessionState

## Description

## TL;DR

Replaces the legacy `state: dict[str, Any]` pattern in `omicsclaw/interactive/interactive.py` with a typed `SessionState` dataclass — 9 documented fields, 3 documented transition methods, and `/tips`-aligned validators. After migration: **0 `state[`** and **0 `state.get(`** accesses in the file, replaced by **88 typed `state.<field>`** accesses.

## Why

Per the friction map for the interactive module: state was a string-keyed dict whose schema lived implicitly across ~90 access sites scattered through 1700+ lines. Each consumer had to know the keys (`session_metadata`, `pipeline_workspace`, `tips_level`, …), and invariants (which keys can be absent, what valid values are) were enforced only by convention.

The original Phase 2 plan expected migrating `tui.py` and 6 `_*_support.py` files, but the **inventory in Task 2.1 revealed the dict-state pattern was contained to `interactive.py`** — `tui.py` and the support modules use other state representations. The migration was therefore one-file.

## Approach (TDD red-green increments)

| # | Commit | Role |
|---|---|---|
| 1 | `ccd9ed9` | inventory: enumerate every read/write site, document 9-key surface, identify 5 invariants |
| 2 | `346d64b` | TDD: 12 SessionState invariant tests + dataclass impl with `from_dict`/`to_dict` adapters for staged migration |
| 3 | `42eb633` | mechanical migration: 15 helper signatures + 90+ access sites in interactive.py + 4 test fixture updates |
| 4 | `7a1309c` | drop the dict adapters — never had a real consumer (migration was direct, not staged) |
| 5 | `bf77524` | fix code-review M1/M2: align `tips_level` default+validator with the actual `/tips level` accepted values (`basic|expert`); route call sites through `stop()` / `set_tips()` / `set_pipeline_workspace()` instead of direct field assignment |

## SessionState shape

```python
@dataclass
class SessionState:
    # required
    session_id: str
    workspace_dir: str
    ui_backend: str          # "cli" or "tui"
    # optional with documented defaults
    pipeline_workspace: str = ""
    session_metadata: dict[str, Any] = field(default_factory=dict)
    messages: list[dict[str, Any]] = field(default_factory=list)
    running: bool = True
    tips_enabled: bool = True
    tips_level: str = "basic"   # validated to {basic, expert}

    def stop(self) -> None: ...
    def set_tips(self, *, enabled=None, level=None) -> None: ...
    def set_pipeline_workspace(self, workspace: str | None) -> None: ...
```

The module is intentionally free of imports from other `interactive/` submodules to avoid circular imports; the "refresh `session_metadata` after `pipeline_workspace` changes" half of the invariant lives in `_set_active_pipeline_workspace` (which calls into `_session_command_support.build_session_metadata`).

## Code review (5-axis, independent agent)

Pre-fix verdict: Approve with conditions. Found:
- M1: `tips_level` default + validator drift (would have changed telemetry default + made the dataclass invariant lie about reality)
- M2: transition methods shipped but never called (interface not enforced)

Both fixed in `bf77524`. Re-running 5-axis review post-fix shows no remaining blockers.

## Verification

- 30/30 across new `tests/test_session_state.py` (8 invariants) + `tests/test_interactive_loop.py` (17) + `tests/test_interactive_omicsclaw_actions.py` (5)
- Full PR test sweep (the 18-test list plus snapshot/lazy-registry/SessionState) → green pre-merge

## What stays unchanged

- `tui.py` and all `_*_support.py` files — they don't use the dict-state pattern, so no migration was needed (verified by inventory in Task 2.1).
- `_session_command_support.build_session_metadata` continues to live there; SessionState does not absorb it (would create a circular import with no leverage gain).
- Public CLI behavior: `/tips`, `/resume`, `/doctor`, `/usage`, etc. — unchanged.

## Risk notes

- The `tips_level` default fix changes a value (`"verbose"` → `"basic"`) that *only the post-migration code briefly held*. Pre-migration runtime always defaulted to `"basic"`. So this is restoring legacy behavior, not breaking it.
- `_VALID_TIPS_LEVELS = {"basic", "expert"}` — if a future PR adds a new level (e.g. `"off"` to suppress tips), update both the validator and the slash-command's whitelist together; otherwise `set_tips` will raise `ValueError` and the slash-command's try/except will print the usage hint.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7988534a5af7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.