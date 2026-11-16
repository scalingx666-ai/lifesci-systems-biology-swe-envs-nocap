# Issue

**Title:** fix(report): write_replot_hint backward compat + crash guard

## Description

## Summary
- `write_replot_hint()` 签名从 3 参数改成 2 参数后，~25 个 skill 调用方没同步更新，导致 bot 运行 skill 时在最后一步抛 `TypeError` 崩溃
- 加 `_r_enhanced_plots=None` 可选参数兼容所有旧调用
- 整体包 `try/except`，确保这个纯信息性 helper 永远不会让 skill 进程崩溃（分析结果在此之前已保存）

## Test plan
- [ ] `python omicsclaw.py run sc-qc --demo` 正常完成不报错
- [ ] 检查 result.json 中 replot hint 正常写入
- [ ] 其他传 3 参数的 skill（sc-filter, sc-preprocessing 等）同样不报错

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added four new single-cell skills: sc-fastq-qc, sc-count, sc-multi-count, and sc-velocity-prep.
* **Bug Fixes**
  * Made report generation more robust by suppressing unexpected errors to avoid crashes.
  * Improved skills table so counts reflect canonical entries, yielding more accurate displayed totals.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6f3ee83563e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.