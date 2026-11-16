# Issue

**Title:** feat(bot): replot_skill tool + environment error UX

## Description

## Summary

- **replot_skill bot tool**: LLM can now call `replot_skill` to re-render R Enhanced (ggplot2) plots from existing skill output without re-running the analysis. Previously the bot would either re-run the full skill or write ad-hoc Python code.
- **Environment error classification**: Raw Python tracebacks replaced with structured, actionable messages that tell users what's wrong and exactly how to fix it.

## Changes

### `omicsclaw/runtime/bot_tools.py`
- New `replot_skill` ToolSpec: LLM knows to use it when user wants R Enhanced plots from existing output; `output_dir` can be omitted (auto-resolved from session history)

### `bot/core.py`
- `execute_replot_skill`: validates output_dir → checks `figure_data/` exists → runs `omicsclaw.py replot` → returns figures via `pending_media`
- `_resolve_last_output_dir`: fallback lookup of most recent successful output dir from session memory
- `_classify_env_error`: detects numpy conflict, missing packages, R not found, OOM, disk full; returns user-friendly message instead of raw traceback
- `_extract_env_snippet`: shows head + tail of stderr (head = offending package, tail = error type)
- `_extract_fix_hint`: actionable per-error command (e.g. `pip install 'numpy<2'`; auto-extracts module name from `ModuleNotFoundError`)
- Wired into `execute_omicsclaw`, `execute_replot_skill`, `execute_parse_literature`

### `omicsclaw/runtime/context_layers/__init__.py`
- Failure Diagnosis rule: LLM relays the fix command directly; does not suggest re-uploading data

## User-facing behavior

**replot flow:**
```
User: run sc-qc
Bot:  [omicsclaw tool] → output: /workspace/.../sc_qc_20260415/

User: make the plots prettier with R Enhanced
Bot:  [replot_skill(skill='sc-qc', output_dir='...')] → reads figure_data/ → returns ggplot2 figures
      ✅ no re-run
```

**Environment error (before → after):**
```
Before: sc-qc failed (exit 1):
        Traceback...ImportError: compiled using NumPy 1.x...

After:  **环境错误（不是你的数据问题）: NumPy 版本冲突**
        分析环境有配置问题，你的数据文件完全没问题。
        修复方法（在终端运行）: pip install 'numpy<2'
        技术详情: [head of traceback showing pyarrow] ... [tail with error type]
```

## Test plan
- [ ] `_classify_env_error` unit tests: 9/9 patterns pass (numpy, ModuleNotFoundError, R, OOM, disk, normal errors not triggered)
- [ ] `_extract_fix_hint` tests: correct commands for all error types including auto-extracted package names
- [ ] `replot_skill` error paths: missing output_dir, missing figure_data/, subprocess failure all return clear messages
- [ ] Integration: replot executor correctly routes subprocess returncode to env error classifier

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Replot Skill: Regenerate figures from existing analyses with customizable rendering options, including renderer selection, plot dimensions, font size, palette, and title adjustments.

* **Improvements**
  * Enhanced error diagnostics providing clearer, more actionable guidance for environment and configuration issues.
  * Automatic detection and reporting of common runtime failures including package conflicts and resource constraints.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42277f33ef78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.