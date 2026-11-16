# Issue

**Title:** 修复 OpenAI-compatible 工具调用链中的 schema 与 tool output 历史问题

## Description

## 变更说明

这次 PR 修复了 bot / interactive 在 OpenAI-compatible 接口下的两类工具调用问题：

1. 修复 `create_csv_file` 工具 schema 不完整的问题
- 为 `data` 数组参数补充 `items` 定义
- 避免在更严格的 OpenAI-compatible 服务端上报错：
  `array schema missing items`

2. 修复多次 tool call 场景下历史消息不完整的问题
- 调整 tool history 清洗逻辑
- 只有当一组 assistant `tool_calls` 与对应的全部 `tool` 输出都完整时才保留
- 避免再次请求模型时出现：
  `No tool output found for function call ...`

3. 补充并稳定回归测试
- 增加所有 array schema 必须声明 `items` 的检查
- 增加 `create_csv_file` schema 的定向测试
- 增加多 tool call 历史完整/不完整两类测试
- 修正旧测试中对 legacy alias `vcf-ops` 的不稳定断言，改为检查 canonical skill 名称

## 验证

已完成以下验证：

- `python -m pytest -q bot/tests/test_tools.py`
- 结果：`5 passed`

另外还做了真实接口验证：
- 使用 DashScope OpenAI-compatible 接口对普通聊天请求测试成功
- 携带 `TOOLS` 的请求返回 `200 OK`
- 未再出现 `create_csv_file` schema 的 400 错误

## 影响范围

主要影响 LLM 工具调用链：
- bot
- `oc interactive`

不影响直接运行技能的命令，例如：
- `oc run <skill> --demo`
- `oc run <skill> --input ...`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ced33e62de0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.