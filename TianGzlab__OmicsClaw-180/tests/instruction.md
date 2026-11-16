# Issue

**Title:** fix(cli): restore subcommand help for oc run/mcp/etc (OMI-10)

## Description

## Summary

`OmicsClawParser` overrode `print_help()` for a curated top-level help, but argparse copies the parser class to every subparser created via `add_subparsers`. Every `oc <command> --help` therefore re-rendered the top-level help instead of the subcommand's argparse output.

Gate the custom help on an `is_root` flag set only on the root parser; subparsers fall through to argparse's default `print_help`.

## Verification

```text
oc run --help                  # shows run options (--demo, --input, --output, ...)
oc mcp --help                  # shows {list,add,remove,config}
oc mcp add --help              # shows name/command/--transport/--env
oc knowledge search --help     # shows query/--domain/--type/--limit
oc auth login --help           # shows provider choices
oc --help                      # still renders curated top-level help
oc                             # still renders curated top-level help
oc version                     # OmicsClaw 0.1.1
```

Closes OMI-10.

## Test plan
- [x] `oc run --help` shows run-level args (not top-level help)
- [x] `oc mcp --help`, `oc mcp add --help` show their own help
- [x] `oc --help` and bare `oc` still show curated top-level help
- [x] `oc version` still works

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f7125b889bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.