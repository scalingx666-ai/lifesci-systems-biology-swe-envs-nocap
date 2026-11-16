# Issue

**Title:** Polish scRNA marker ranking workflow and gallery

## Description

## Summary
- refactor `sc-markers` to follow the singlecell skill template and output contract
- use normalized `adata.X` consistently for public marker ranking instead of silently preferring `adata.raw`
- add stronger preflight guidance for grouping column selection and beginner next-step hints
- replace the old marker figures with a richer marker gallery and figure-data exports
- add dedicated `sc-markers` tests and align docs / knowhow / registry

## Validation
- `python -m pytest -q skills/singlecell/scrna/sc-markers/tests/test_sc_markers.py tests/test_sc_preflight.py tests/test_knowhow.py tests/test_registry.py`
- smoke outputs generated under:
  - `output/review_sc_markers`
  - `output/review_sc_markers_ttest`
  - `output/review_sc_markers_logreg`

## Notes
- `markers_dotplot.png` is now a custom block-ordered dotplot grouped by the source cluster of each top marker, rather than a default Scanpy-reordered view.
- when filtered rank-gene results are empty, the wrapper now falls back to unfiltered results instead of crashing or exporting an empty gallery.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added five marker visualization plots: heatmap, dotplot, effect summary, cluster summary, and fraction scatter.
  * Introduced filtering parameters (`--min-in-group-fraction`, `--min-fold-change`, `--max-out-group-fraction`) for refined marker selection.
  * Automatic grouping column detection when not explicitly provided.

* **Changes**
  * Output artifact renamed to `processed.h5ad` with restructured table and figure outputs.
  * Marker discovery now defaults to normalized expression instead of raw counts.
  * Enhanced validation and guidance during marker analysis workflow.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `baf44201fd0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.