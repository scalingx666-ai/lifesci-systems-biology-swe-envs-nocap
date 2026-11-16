# Issue

**Title:** fix(review): apply CodeRabbitAI recommendations from PR #178

## Description

Three issues addressed:

1. omicsclaw.py — move _configure_stdio_error_handling() from module level into main().  Module-level invocation ran on every import, including during test-suite execution, and could silently change the error-handler on pytest's own captured streams (TextIOWrapper objects that do expose reconfigure()).  Calling it only from main() keeps the fix fully effective for the CLI while eliminating the import-time side-effect.  Also replace `streams or fallback` idiom with an explicit `if streams else fallback` for readability.

2. tests/test_scrna_console_encoding.py — add Iterator[str] return-type annotation on _iter_string_fragments().  The generator was the only helper missing a type hint.

3. bot/core.py — remove redundant `import re as _re` inside the "there is no package called" branch; the top-level `import re` (line 8) is already in scope.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0726141a62ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.