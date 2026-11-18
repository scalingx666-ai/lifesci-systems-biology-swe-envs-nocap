# Issue

**Title:** Improve the Gurobi support in MICOM

## Description

This improves the Gurobi support in MICOM by adjusting the numerical handling and explicit use of faster primal accessors. 

## Changes

- follow the best practices from the [Gurobi Numerical Issue Guidelines](https://www.gurobi.com/documentation/9.5/refman/guidelines_for_numerical_i.html)
- faster accessors for primal values (obtaining primal values now takes <1s even for large models)
- delegate the objective scaling to Gurobi

## ToDo

- [x] wait for 
- [ ] implement a smaller example model to integrate Gurobi into the CI, the free license is limited to <200 variables for QPs
- [x] ask @RichardOberdieck if it is okay to mention him in the docs

## Benchmark

Simple benchmark for the Cancer1 model:

```
In [84]: com.optimize()                                                                                                                                                       
Out[84]: <CommunitySolution 0.493 at 0x7f9a23a1a820>                                                                                                                          
                                                                                                                                                                              
In [85]: %time x = com.solver.primal_values                                                                                                                                   
CPU times: user 141 ms, sys: 12.4 ms, total: 154 ms                                                                                                                           
Wall time: 153 ms                                                                                                                                                             
                                                                                                                                                                              
In [86]: %time sol = com.cooperative_tradeoff(fraction=0.5, fluxes=True)                                                                                                      
CPU times: user 26 s, sys: 62.6 ms, total: 26.1 s                                                                                                                             
Wall time: 26.1 s 
```

This took ~30 minutes before.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ccb1218bbd0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.