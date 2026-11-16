# Issue

**Title:** docs: move to scverse-doc and adopt the shared scverse docs TOC

## Description

Switches the docs from sphinx-book-theme to scverse-doc and groups the sidebar into Getting started, Guides, Reference and Project as agreed in scverse/scverse-doc#62, with a new citation page, muon's aquamarine accent from the registry and the muon-tutorials notebooks included under Guides instead of linked out.
The tutorials submodule points at scverse/muon-tutorials#9, which fixes broken links that would fail the -W build, and should move to its default branch once that is merged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb4666ee7c04`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.