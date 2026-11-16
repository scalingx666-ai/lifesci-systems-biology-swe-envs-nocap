# Issue

**Title:** Simplify configuration

## Description

This makes the client and server independent of the global `config.json` file. This simplifies configuration by automating it into 2 configurations:
- development (run on localhost)
- production (run on scope.aertslab.org)
Further configurations can be added as necessary.
The major advantages of these changes are:
1. No more manually editing `config.json`
1. No more confusion between client config and server config

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `232e0762b690`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.