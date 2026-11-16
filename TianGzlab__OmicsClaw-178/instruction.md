# Issue

**Title:** refactor(skill-loader): fix issues found in OMI-2 evaluation

## Description

## Summary

OMI-2 评估发现的 skill 加载机制问题修复（[评估全文](mention://issue/6eb91e7d-73a5-4c7d-9e82-33b3713d650f)），全部局部修复，无架构改动。

- **Singleton 收口**：`capability_resolver` / `agents.tools` / `notebook_session` / `kernel_manager` 不再各自 `OmicsRegistry()` + `load_all()`，统一走 `ensure_registry_loaded()`。chat-turn warm path **430 ms → 2 ms（170×）**。
- **`_loaded` 与 `skills_dir` 绑定**：换目录会触发 rescan 而不是悄悄返回旧快照；新增 `invalidate()` / `reload()` 让 app-server / interactive 不必重启就能感知 SKILL.md 变化。
- **删掉 `_HARDCODED_DOMAINS.skill_count` 字面量**：singlecell 表里写 14、实际 30 的死状态清掉，`_refresh_domain_skill_counts` 永远从磁盘算。
- **`scripts/generate_catalog.py` 换 `yaml.safe_load`**：与 `lazy_metadata` 对齐，消除手写 YAML 解析的潜在分歧。catalog.json byte-identical。
- **YAML 解析失败 `logger.warning`**：SKILL.md / parameters.yaml 不再静默降级。
- **`skills/singlecell/_lib/__init__.py` PEP 562 lazy-load**：包级导入不再触发 `import scanpy`（scripts 自身的顶层 import 是另外的事）。
- **新增 `tests/test_registry_discovery.py`**：10 条 — 启发式负面用例、fixture 隔离、cache key、invalidate/reload、`parameters.yaml` domain 优先级、`skill_count` 从盘读取。

## Test plan

- [x] `python -m pytest tests/test_registry*.py tests/test_generate_catalog.py tests/test_skill_listing.py tests/test_skill_metadata_contract.py tests/test_capability_resolver.py tests/test_interactive_*.py tests/test_keyword_routing.py tests/test_diagnostics.py -q` → **267 passed**
- [x] `python omicsclaw.py list` → 89/175 entries
- [x] `python scripts/generate_catalog.py --check` → up to date
- [x] capability_resolver cold→warm perf：430 ms → 2.4 ms（5 次平均）
- [x] 宽测试：117 → 114 failing（均为预先存在的 env / snapshot drift，未新引入）

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added registry reload and invalidation capabilities to detect filesystem changes
  * Introduced lazy-loading for skill submodules to improve startup performance

* **Bug Fixes**
  * Registry now properly caches results and invalidates on directory changes
  * YAML parsing errors are now logged as warnings instead of being silently ignored

* **Documentation**
  * Updated architecture documentation to clarify skill count computation

* **Tests**
  * Added comprehensive test coverage for registry discovery and caching behavior

[![Review Change Stack](https://storage.googleapis.com/coderabbit_public_assets/review-stack-in-coderabbit-ui.svg)](https://app.coderabbit.ai/change-stack/TianGzlab/OmicsClaw/pull/178)

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a73f7e3e57f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.