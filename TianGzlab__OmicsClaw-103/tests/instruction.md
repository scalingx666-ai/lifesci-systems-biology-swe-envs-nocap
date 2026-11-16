# Issue

**Title:** Complete architecture contract documentation

## Description

## TL;DR

Completes the remaining architecture optimization follow-up by making the domain input contracts and framework contract specs tracked, discoverable, and protected by lightweight tests.

## Review Order

1. `tests/test_domain_input_contracts.py` and `tests/test_engineering_contract_docs.py` - new guardrails that prevent local-only ignored contract docs.
2. `docs/engineering/domain-input-contracts.md` - factual input contracts for all registered domains.
3. `docs/engineering/2026-05-07-*.md` - architecture contract specs for runner, output ownership, alias ownership, bot runner, skill help, and roadmap.
4. `README.md` and `.gitignore` - links and allowlist for tracked contract docs while keeping unrelated local notes ignored.

## Diff Buckets

- Contract docs: `docs/engineering/*.md`
- Guardrail tests: `tests/test_domain_input_contracts.py`, `tests/test_engineering_contract_docs.py`
- Contributor discovery/wiring: `README.md`, `.gitignore`

## Risk Notes

- Runtime behavior is unchanged.
- The `.gitignore` change is intentionally narrow: it continues ignoring local `docs/engineering/2026-05-07-*.md` scratch notes except the six formal architecture contract specs, plus the domain input contract doc.
- Tests call `git ls-files` by design to catch the exact previous failure mode where docs existed locally but were not tracked.

## Verification

```bash
conda run -n OmicsClaw python -m pytest tests/test_domain_input_contracts.py tests/test_engineering_contract_docs.py tests/test_documentation_facts.py tests/test_skill_runner_contract.py tests/test_skill_metadata_contract.py tests/test_skill_help_contract.py tests/test_registry_alias_contract.py tests/test_output_ownership_contract.py tests/test_bot_runner_contract.py tests/test_execution_default_executor.py tests/test_execution_executors.py tests/test_execution_subprocess_executor.py tests/test_skill_run_result.py -q
# 145 passed in 187.96s

conda run -n OmicsClaw python -m compileall -q tests/test_domain_input_contracts.py tests/test_engineering_contract_docs.py

git diff --check upstream/main..HEAD

graphify update .
```

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Documentation**
  * Added comprehensive engineering architecture contracts defining component interactions, ownership boundaries, and specification requirements across the system.
  * Updated developer notes with clarification on shared result construction and references to architecture contracts.

* **Tests**
  * Added validation tests ensuring documentation completeness and accuracy with respect to registered components.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `899240ddde21`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.