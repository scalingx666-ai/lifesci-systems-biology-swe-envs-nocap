# Issue

**Title:** Add rules for Diamond (blastp) and Prodigal

## Description

Four new rules proposed, with no new software dependencies.

1. run_prodigal - predicts ORFs on contigs rather than assembled genomes (perhaps could be renamed to contig_prodigal to avoid confusion)
2. run_blastp - takes contig ORFs as input, uses the Diamond Blastp Snakemake wrapper: https://github.com/snakemake/snakemake-wrappers/tree/0.80.1/bio/diamond/blastp
3. binning - calls the outputs from concoct, metabat, and maxbin
4. binEvaluation - calls the outputs from binRefine and binReassembly

The parsing rules for binning and binEvaluation may be iffy - I tested on a login node, rather than as a cluster job.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `677f4b88e24d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.