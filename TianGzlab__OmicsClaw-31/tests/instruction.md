# Issue

**Title:** refactor: consolidate orchestrators and clean up deprecated code

## Description

## Summary

This PR consolidates all domain-specific orchestrators into a unified `omics_orchestrator`, significantly simplifying the codebase architecture.

## Changes

**Removed orchestrators** (5 files, -1785 lines):
- `skills/genomics/orchestrator/genomics_orchestrator.py`
- `skills/metabolomics/orchestrator/metabolomics_orchestrator.py`
- `skills/proteomics/orchestrator/proteomics_orchestrator.py`
- `skills/singlecell/scrna/orchestrator/sc_orchestrator.py`
- `skills/spatial/orchestrator/spatial_orchestrator.py` + SKILL.md + tests

**Updated**:
- `omicsclaw/core/registry.py` - removed references to deleted orchestrators
- `omicsclaw.py` - cleaned up imports
- `pyproject.toml` - removed unused dependency
- `tests/test_registry.py` - updated to reflect consolidation
- Documentation: `README.md`, `LLM_ROUTING_GUIDE.md`, `architecture-analysis.md`

## Rationale

The previous architecture maintained separate orchestrators for each omics domain (genomics, proteomics, metabolomics, single-cell, spatial), leading to code duplication and maintenance overhead. The unified `omics_orchestrator` in `skills/orchestrator/` now handles routing across all domains, providing:

- Single source of truth for orchestration logic
- Easier maintenance and updates
- Consistent behavior across all omics domains
- Reduced codebase complexity (-1785 lines)

## Test plan

- [ ] Run `python omicsclaw.py list` to verify all skills are still registered
- [ ] Test orchestrator routing: `python omicsclaw.py run orchestrator --demo`
- [ ] Verify domain-specific skills still work (spatial, single-cell, genomics, etc.)
- [ ] Run full test suite: `pytest tests/`

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b14a1cc12c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.