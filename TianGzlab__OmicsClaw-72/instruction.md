# Issue

**Title:** Accept --r-enhanced flag in all 29 scRNA skills

## Description

## Summary
Previously 7 skills crashed with `unrecognized arguments: --r-enhanced` because they didn't define this argparse flag. Now all 29 scRNA skills accept `--r-enhanced` — the 7 upstream/utility skills accept it as a silent no-op.

**Problem:** Users don't know which skills support R Enhanced, and passing `--r-enhanced` to unsupported skills caused a crash.

**Fix:** Add `--r-enhanced` as `store_true` to the 7 remaining skills with help text explaining no R Enhanced plots are available.

## Test plan
- [x] sc-count --demo --r-enhanced: passes (was crashing)
- [x] sc-fastq-qc --demo --r-enhanced: passes
- [x] sc-velocity-prep --demo --r-enhanced: passes

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Added `--r-enhanced` flag support across single-cell analysis tools for CLI consistency.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd9209d06d7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.