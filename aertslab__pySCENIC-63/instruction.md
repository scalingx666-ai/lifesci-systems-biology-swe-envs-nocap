# Issue

**Title:** CLI: Fix for load_adjacencies with specific gene names

## Description

With some gene names ("nan"), the load_adjacencies function gives a mix of str and float types in the `TF` and/or `targets` column, which causes the following issue in the `ctx` step:

```
$ pyscenic ctx adj.tsv dm6-5kb-upstream-full-tx-11species.mc8nr.feather --annotations_fname motifs-v8-nr.flybase-m0.001-o0.0.tbl --expression_mtx_fname LRRK.loom --cell_id_attribute CellID --gene_attribute Gene --mode "dask_multiprocessing" --output reg.csv --num_workers 20
/usr/local/lib/python3.6/site-packages/dask/config.py:161: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please re
ad https://msg.pyyaml.org/load for full details.
  data = yaml.load(f.read()) or {}
/usr/local/lib/python3.6/site-packages/distributed/config.py:20: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Ple
ase read https://msg.pyyaml.org/load for full details.
  defaults = yaml.load(f)
2019-03-18 11:21:26,055 - pyscenic.cli.pyscenic - INFO - Creating modules.
2019-03-18 11:21:27,154 - pyscenic.cli.pyscenic - INFO - Loading expression matrix.
Traceback (most recent call last):
  File "/usr/local/bin/pyscenic", line 10, in <module>
    sys.exit(main())
  File "/usr/local/lib/python3.6/site-packages/pyscenic/cli/pyscenic.py", line 402, in main
    args.func(args)
  File "/usr/local/lib/python3.6/site-packages/pyscenic/cli/pyscenic.py", line 129, in prune_targets_command
    modules = adjacencies2modules(args)
  File "/usr/local/lib/python3.6/site-packages/pyscenic/cli/pyscenic.py", line 98, in adjacencies2modules
    keep_only_activating=(args.all_modules != "yes"))
  File "/usr/local/lib/python3.6/site-packages/pyscenic/utils.py", line 264, in modules_from_adjacencies
    rho_threshold=rho_threshold, mask_dropouts=rho_mask_dropouts)
  File "/usr/local/lib/python3.6/site-packages/pyscenic/utils.py", line 129, in add_correlation
    col_idx_pairs = _create_idx_pairs(adjacencies, ex_mtx)
  File "/usr/local/lib/python3.6/site-packages/pyscenic/utils.py", line 71, in _create_idx_pairs
    sorted_genes = sorted(genes)
TypeError: '<' not supported between instances of 'float' and 'str'
```

This fixes the problem from the read_csv side, but there may be a better way to handle this.  This was tested and working in a Drosophila dataset.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `486d602f2d70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.