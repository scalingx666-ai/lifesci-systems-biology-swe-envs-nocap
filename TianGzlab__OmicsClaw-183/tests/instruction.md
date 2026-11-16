# Issue

**Title:** refactor(skill-template): rebuild templates/skill/ as runnable human-copy starter

## Description

## Summary

The previous `templates/skill/` was a doc-only scaffold: empty `tests/`, no `.py` script, 30-line methodology stub, `parameters.yaml` missing the soft fields every gold skill carries. The SKILL.md preamble also claimed three consumers (humans, `omics-skill-builder`, `migrate_skill.py`) but the two codegen scripts have their own internal renderers and never read this directory.

This PR reshapes the template around a single consumer — humans copying the directory — and lifts it close enough to `skills/singlecell/scrna/sc-de` and `skills/spatial/spatial-de` that `cp -r` + rename leaves the new skill ~80% complete.

## What changed

- **Runnable `replace_me.py`** — argparse + in-memory synthetic CSV demo + common report-helper calls. Writes `tables/replace_me.csv` + `report.md` + `result.json`.
- **`tests/test_replace_me.py`** — `test_demo_mode` + result-envelope assertion. `.gitkeep` → `__init__.py`.
- **`templates/skill/README.md`** (new) — bootstrap steps, the lint rules every v2 skill must pass, and the soft conventions the template cannot scaffold (`skills/<domain>/_lib/` shared helpers, `<skill>/data/` real fixtures, optional `r_visualization/` layer).
- **`SKILL.md`** — 30-line HTML authoring block compressed to a 5-line checklist; false codegen-consumer claim removed; `requires: [pyyaml]` residue dropped from frontmatter.
- **`parameters.yaml`** — gains the soft fields all gold skills carry (`requires`, `install`, `os`, `homepage`, `emoji`), each annotated with what consumes it.
- **`references/methodology.md`** — rewritten as a 4-section skeleton (Capabilities / Workflow / Methodology / Dependencies) plus HTML-commented optional sections.
- **`references/output_contract.md`** — tightened to minimal core plus opt-in blocks for `processed.h5ad` / `figures/` / `figure_data/` / `reproducibility/`.
- **`references/parameters.md`** — regenerated from the new sidecar.
- **`docs/adr/0003-skill-template-is-human-copy-only.md`** (new) — documents the scope decision (codegen scripts are NOT refactored to read the template; structural drift is caught by `skill_lint.py` instead).

## Verification

- `python scripts/skill_lint.py templates/skill` → `ok`
- `python templates/skill/replace_me.py --demo --output /tmp/replace_me_demo` → runs end-to-end, produces all claimed paths
- `pytest templates/skill/tests/` → 2 passed
- `skills/singlecell/scrna/sc-de` and `skills/spatial/spatial-de` still lint clean (no regression)

## Test plan

- [ ] Reviewer runs `scripts/skill_lint.py templates/skill` and confirms `ok`
- [ ] Reviewer runs `python templates/skill/replace_me.py --demo --output /tmp/demo` and confirms the three baseline artifacts (`report.md`, `result.json`, `tables/replace_me.csv`) are written
- [ ] Reviewer runs `pytest templates/skill/tests/` and confirms both tests pass
- [ ] Reviewer sanity-reads `templates/skill/README.md` and the new ADR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe4cf5bf37bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.