# Issue

**Title:** Add a more permissible media completion

## Description

The medium completion functions now have a flag that allows adding additional flux
to components already in the candidate medium. The default is now changed to that
new non-strict mode which makes it much easier and more efficient to complete media.
In that case the `max_added_import` amount now specifies the maximum flux added on top
the limit specified in the candidate medium.

```
In [1]: import micom as mm

In [2]: com = mm.Community(mm.data.test_taxonomy())
Building ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:00

In [3]: med = mm.media.minimal_medium(com, 0.85, 0.85)

In [4]: med
Out[4]: 
EX_glc__D_m    10.000000
EX_nh4_m        4.634880
EX_o2_m        20.757401
EX_pi_m         3.126895
dtype: float64

In [5]: co = mm.media.complete_medium(com, growth=0.95, min_growth=0.95, medium=med, strict=med.index)  # old
[18:43:53] WARNING  solver encountered an error infeasible                                                                                                                              solution.py:220
---------------------------------------------------------------------------
OptimizationError                         Traceback (most recent call last)
Input In [5], in <cell line: 1>()
----> 1 co = mm.media.complete_medium(com, growth=0.95, min_growth=0.95, medium=med, strict=med.index)

File ~/code/micom/micom/media.py:380, in complete_medium(model, medium, growth, min_growth, max_import, minimize_components, weights, strict)
    378             sol = None
    379 if sol is None:
--> 380     raise OptimizationError(
    381         "Could not find a solution that completes the medium :("
    382     )
    383 completed = pd.Series(dtype="float64")
    384 for rxn in model.exchanges:

OptimizationError: Could not find a solution that completes the medium :(

In [6]: co = mm.media.complete_medium(com, growth=0.95, min_growth=0.95, medium=med)  # new

In [7]: co
Out[7]: 
EX_fru_m        0.965127
EX_glc__D_m    11.000000
EX_gln__L_m     0.272640
EX_nh4_m        4.634880
EX_o2_m        20.757401
EX_pi_m         3.494765
dtype: float64

In [8]: co - med
Out[8]: 
EX_fru_m           NaN
EX_glc__D_m    1.00000
EX_gln__L_m        NaN
EX_nh4_m       0.00000
EX_o2_m        0.00000
EX_pi_m        0.36787
dtype: float64
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `591c7a48e2d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.