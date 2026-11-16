# Issue

**Title:** Migrate logo assets to high-resolution SVG

## Description

## Summary
- migrate README/docs logo assets from JPEG/PNG to high-resolution SVG
- replace mislabeled SVG files that contained JPEG bytes with real SVG assets
- update English and Chinese README logo references to the SVG asset

## Verification
- `xmllint --noout docs/images/OmicsClaw_logo.svg docs/images/OmicsClaw_icon.svg docs/logo/light.svg docs/logo/dark.svg docs/favicon.svg website/public/favicon.svg`
- `grep -RInE '<image|data:image|base64|xmlns:v|fill="None"|stroke="None"|<<<<<<<|>>>>>>>' docs/images/OmicsClaw_logo.svg docs/images/OmicsClaw_icon.svg docs/logo/light.svg docs/logo/dark.svg docs/favicon.svg website/public/favicon.svg || true`
- `convert docs/images/OmicsClaw_logo.svg -resize 380x /tmp/backend-omicsclaw-logo-380.png`
- `convert docs/images/OmicsClaw_icon.svg -resize 128x128 /tmp/backend-omicsclaw-icon-128.png`
- `convert website/public/favicon.svg -resize 48x48 /tmp/backend-website-favicon-48.png`
- `git diff --check upstream/main..HEAD`

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Documentation**
  * Updated README and Chinese README files to reference the OmicsClaw logo in SVG format instead of JPEG.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21c84e3923c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.