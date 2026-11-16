# Issue

**Title:** refactor(deps): empty singlecell extra, delegate to sub-extras

## Description

## Summary

- `singlecell = []` — 清空重复包列表
- 原来的 12 个包全部已有对应子 extra 覆盖（`singlecell-doublet`、`singlecell-batch`、`singlecell-annotation`、`singlecell-pseudotime` 等）
- 需要完整安装请用 `pip install -e ".[singlecell-full]"`

## Background

原 `singlecell` extra 是各子 extra 的重复集合，且在 Windows 上会触发 `annoy`（bbknn 依赖）和 `hnswlib`（scanorama/pyVIA 依赖）的 C++ 编译失败。清空后用户按需选择子 extra，避免不必要的编译依赖。

## Test plan

- [ ] `pip install -e ".[singlecell]"` 只装 Tier 1 core，无额外包
- [ ] `pip install -e ".[singlecell-full]"` 仍可正常装全套
- [ ] `pip install -e ".[singlecell-batch]"` 单独装 batch 子模块正常

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * The `singlecell` optional-dependencies extra is now empty. Previously it bundled scRNA-seq analysis packages for doublet detection, batch integration, cell annotation, gene regulatory network inference, pseudotime/velocity analysis, differential expression analysis, and clustering backends. These dependencies will no longer be automatically installed with the `singlecell` extra.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07140a2565ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.