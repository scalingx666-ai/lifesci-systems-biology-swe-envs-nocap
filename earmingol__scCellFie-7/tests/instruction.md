# Issue

**Title:** Update to phenylalanine-associated tasks

## Description

Merged Phenylalanine to phenylacetyl-L-glutaminate onto Phenylalanine to phenylacetaldehyde

Phenylalanine to phenylacetyl-L-glutaminate only had reactions ALDD19xr (r0545), PHYCBOXL, and PEAMNO, which are the same ones defining Phenylalanine to phenylacetaldehyde. The latter only had PHYCBOXL, and PEAMNO here, which is incomplete.

Reactions that should be in Phenylalanine to phenylacetyl-L-glutaminate are ALDD19xr (r0545), PACCOAL and PHACCOAGLNAC. However, the last two are not linked to human/mouse enzymes and seem to happen only in microbes (https://pubmed.ncbi.nlm.nih.gov/36549300/).

![Screenshot 2025-02-18 at 11 08 53](https://github.com/user-attachments/assets/f146a684-7c0f-46b0-8610-b667c664850e)

For this reason, only keeping the Phenylalanine to phenylacetaldehyde task, including ALDD19xr (r0545), PHYCBOXL, and PEAMNO reactions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c36c8b8e457d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.