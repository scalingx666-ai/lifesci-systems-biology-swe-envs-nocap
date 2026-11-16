# Issue

**Title:** Genome bins

## Description

I added some functionality to QC atac-seq data based on the raw fragment data. Main changes

**Things added**

- Speed up for creating a cellxregions matrix with `count_fragments_features` (~4x) by using the lil_matrix format
- `tss_enrichment` function calculatiing the TSS enrichment score per cell and associated plotting function
- `nucleosome_signal` function calculating the mononucleosomal/nucleosome free ratio of fragments and plotting function
- Utility function to fetch the regions of genes from the rna layer annotation: `get_gene_annotation_from_rna`

**Summary of API**
`
import muon as mu
from muon import atac as ac


data_dir = "/home/max/projects/pbmc_multimodal/PBMC_rep1/"
mdata = mu.read_10x_h5(os.path.join(data_dir, "filtered_feature_bc_matrix.h5"))

rna = mdata.mod["rna"]
atac = mdata.mod["atac"]

genes = mu.utils.get_gene_annotation_from_rna(mdata)


# Nucleosome Signal
ac.tl.nucleosome_signal(mdata, n = 1000000)
atac.obs["NS>4"] = atac.obs.Nucleosome_signal > 4
mu.atac.pl.fragment_histogram(mdata, region='chr1-1-2000000', groupby=['NS>4'])

# TSS enrichment
tss_enrichment = ac.tl.tss_enrichment(mdata, n_tss=2000)
tss_enrichment.obs["Score>2"] = tss_enrichment.obs.TSS_score > 2

ac.pl.tss_enrichment(tss_enrichment, groupby='Score>2')
`


**Caveats and TODO**
- Not sure how to best write the plotting functions. Probably the scanpy functionalities can be used better
- Fetching the reads for nucleosome enrichment is slower than with Signac (they have a cpp implementation) by ~5x

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ad472c12ec5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.