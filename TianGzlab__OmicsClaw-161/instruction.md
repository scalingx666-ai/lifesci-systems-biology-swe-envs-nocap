# Issue

**Title:** feat(memory): derive readable display label for analysis://* nodes

## Description

## Summary

The desktop memory tree currently renders ``edge.name`` (URI's last
path segment) as the entry label. For ``analysis://*`` URIs that
segment is a UUID hex (load-bearing — analysis is overwrite-mode, each
run needs a unique URI), so users see entries like
``3c7a182ee7ab498ea4454a2f8465063c`` and cannot tell **which dataset**,
**when**, or **whether the run succeeded**.

This PR keeps the URI as identity (no migration, lineage references
intact) and derives a Display label from ``Memory.content`` at the API
boundary, surfaced in the same ``name`` field of ``/memory/browse`` and
``/memory/children``. The frontend's existing ``name || path`` fallback
means no UI change is required.

Format:

```
<dataset_basename> · <hh:mm or yyyy-mm-dd hh:mm> · <status>
```

Examples:

| URI | Old name | New name |
|---|---|---|
| ``analysis://sc-preprocessing/3c7a182e…`` | ``3c7a182ee7ab498ea4454a2f8465063c`` | ``pbmc3k_raw.h5ad · 12:43 · failed`` |
| ``analysis://spatial-domains/03a3a402…`` | ``03a3a402cc2a49f3b864e05f6cd128db`` | ``visium_brain.h5ad · 2026-05-05 08:15 · completed`` |

## Approach

Layering and trade-offs are recorded in
``docs/adr/0002-derived-display-label-for-analysis-memory.md`` (local
working doc; not part of this PR). Headlines:

- ``omicsclaw/memory/compat.py::_analysis_content_to_title`` — pure
  helper. Parses JSON, extracts basename of ``parameters.input``,
  formats ``executed_at`` in server-local TZ, appends ``status``.
  Returns ``None`` on any parse failure or missing field — caller
  falls back to ``edge.name`` so the UI never renders blanks.
- ``omicsclaw/app/server.py::_decorate_analysis_titles`` — walks the
  children list returned by ``list_children_rich`` and rewrites
  ``name`` in-place when ``domain == "analysis"``. Full content is
  fetched per child via ``recall`` (``content_snippet`` is truncated
  to 100 chars and may drop ``executed_at``). Cost: N indexed reads
  per tree level on local SQLite, N ≤ 50 in practice — fine for
  desktop usage.
- ``MemoryEngine`` and ``MemoryClient`` are **not modified**. The
  engine keeps its "7 verbs against (uri, namespace) pairs"
  abstraction; analysis-shape knowledge stays in compat.py where it
  already lives.

## Alternatives rejected

- **URI rewrite** (path becomes ``<skill>/<dataset>_<timestamp>``):
  breaks ``parent_analysis_id`` / ``source_analysis_id`` lineage
  references; collisions need UUID anyway.
- **Engine-level derivation**: couples engine to AnalysisMemory shape.
- **Frontend-level derivation**: duplicates JSON shape knowledge in
  TypeScript; other surfaces (CLI memory listing) wouldn't benefit.
- **New ``title`` field**: every consumer of ``name`` would need an
  opt-in; replacing ``name`` is invisible to the existing frontend
  fallback.

## Out of scope

- Sort order. Currently ``Edge.priority asc, edge.name``. The new
  labels may expose a UX gap (alphabetic by title vs ``executed_at
  desc``). Defer until user feedback warrants.
- ``insight://*`` (URI = ``<entity_type>/<entity_id>``) and
  ``project://*`` (URI = ``<uuid_hex>``) follow the same pattern; the
  helper and decoration step are written so extension is additive.
- Remote-mode TZ caveat — backend renders in server TZ; documented in
  the ADR.

## Test plan

- [x] ``tests/memory/test_compat_display_label.py`` — 14 unit tests:
      happy path, all status values, basename extraction (full path /
      bare filename / missing input / missing parameters dict), silent
      fallbacks (non-JSON, empty content, missing ``executed_at``,
      invalid timestamp), today-vs-older boundary
- [x] ``tests/test_app_server.py`` — 3 integration tests over the
      endpoints: ``/memory/browse`` decorates analysis children,
      ``/memory/children`` does too, non-analysis domains untouched
- [x] Full memory regression suite: 335 passed
      (was 318; +14 unit, +3 integration; 0 regressions)
- [ ] Manual: load desktop, navigate to ``analysis://sc-preprocessing``,
      confirm tree shows readable rows instead of UUID hex

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17fd0b80a16f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.