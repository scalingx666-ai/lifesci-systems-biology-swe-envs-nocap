# Issue

**Title:** Avoid FutureWarning from deprecated scanpy.__version__

## Description

## Description

Importing muon emits a `FutureWarning` on recent scanpy versions:

```
muon/_core/preproc.py:31: FutureWarning: `__version__` is deprecated, use `importlib.metadata.version('scanpy')` instead
  if Version(scanpy.__version__) < Version("1.10"):
```

The version guard now queries the installed scanpy version via `importlib.metadata.version("scanpy")` instead of the deprecated `scanpy.__version__`, matching scanpy's own recommendation. The bare `import scanpy` is dropped since every remaining reference uses `from scanpy import ...`.

Verified that `import muon` no longer raises a `FutureWarning` (with `warnings.simplefilter("error", FutureWarning)`) against scanpy 1.12.1, and the `< 1.10` branch selection is unchanged.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58dc672e6089`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.