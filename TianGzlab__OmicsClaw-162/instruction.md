# Issue

**Title:** feat(orchestrator,literature): migrate 3 final skills (PR-G of skill rework)

## Description

## Summary

PR-G — **the FINAL batch** of the 89-skill v2 rework. Migrates the last 3 remaining skills (orchestrator + omics-skill-builder + literature) from legacy SKILL.md to v2 (sidecar `parameters.yaml` + structured `SKILL.md` + `references/`).

The 3 final skills (759 LoC total — different from the analysis-skill family because they are meta / network I/O):

- **orchestrator** (413 lines, `omics_orchestrator.py`) — multi-omics natural-language query routing across 6 routed domains via `keyword` / `llm` / `hybrid` modes. Outputs `result.json` (real query) or `demo_report.txt` (`--demo`) — mutually exclusive.
- **omics-skill-builder** (149 lines, `omics_skill_builder.py`) — scaffolds NEW skills from a NL request via `omicsclaw.core.skill_scaffolder`. Outputs `SCAFFOLD_SUMMARY.md` + `report.md` + `result.json` + the new skill directory under `skills/<domain>/<name>/`.
- **literature** (197 lines, `literature_parse.py`) — parses scientific references (URL / DOI / PubMed / file / text) for GEO accessions, optionally downloads the GEO datasets. Outputs `extracted_metadata.json` + `report.md` + `result.json`.

## With this PR — the catalog is COMPLETE

| Domain | v2 / total |
|---|---|
| singlecell | 29 / 29 |
| spatial | 17 / 17 |
| bulkrna | 13 / 13 |
| genomics | 10 / 10 |
| proteomics | 8 / 8 |
| metabolomics | 8 / 8 |
| **orchestrator** | **2 / 2** |
| **literature** | **1 / 1** |
| framework | 1 / 1 |
| **TOTAL** | **89 / 89 ✓** |

## Quality gates

- `scripts/skill_lint.py --all` → **90 ok / 0 fail / 0 warn** (orchestrator and literature lint at the domain root because their SKILL.md lives there directly).
- `pytest` (10-test sweep) → **210 passed** (was 207 after PR-F; +3 from new auto-discovery roundtrips).
- Independent `code-reviewer` agent: caught **1 Critical** (literature CLI example used `--input-type pdf` but valid choices are `{auto,url,doi,pubmed,file,text}` — would have failed first non-demo invocation) **+ 7 Important** (orchestrator `--routing-mode` semantics, LLM_API_KEY silent fallback, `result.json` schema, `7 → 6` domains, scanpy → pyyaml install dep). All Critical + Important fixed in the amended commit.

### Proactive PR-F regression avoidance — verified by reviewer

The PR-F-discovered classes both verified clean for PR-G after my proactive rewrites:
- **`allowed_extra_flags`** — all 3 yaml files match argparse exactly (orchestrator: 2, omics-skill-builder: 11, literature: 3).
- **`output_contract.md`** — all 3 line anchors match real `.write_text` / `json.dump` / `parser.error` / `sys.exit` calls.

## Test plan

- [ ] CI green on this PR (core-test 3.11 / 3.12, memory-test, bot-core-test, spatial-test, pr-summary, CodeRabbit).
- [ ] CodeRabbit summary cleanly enumerates the 3 SKILL.md migrations.
- [ ] No Claude attribution in commit message or PR body.
- [ ] Mergeable / `MERGEABLE` + `CLEAN` mergeStateStatus.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cef54ddabffa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.