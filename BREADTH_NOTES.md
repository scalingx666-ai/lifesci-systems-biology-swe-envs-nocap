# Build notes - Systems Biology & Network Modeling

Repo2RLEnv pr_diff (v0.9.6), Harbor-format output. Domain: systems-biology.

## Funnel

| Stage | Count |
|---|---|
| Domain candidates (deduped) | 203 |
| After active+star+noise filter | 78 |
| Final target list (cap unlimited) | 78 |
| Repos with >=1 task | 12 |
| Repos with 0 tasks | 61 |
| Total tasks (unlimited (no per-repo cap)) | 337 |

## Generation

- Shared task bank: each repo generated once (pr_diff, limit=3,
  max_files_per_pr=15, min_loc_changed=2), 4-way concurrency,
  rate-limit-aware with .done checkpoint resume.
- Per-domain consolidation: rank by reward_calibration.loc_changed desc,
  keep ALL qualifying tasks (no per-repo cap). Zero-yield repos are NOT fabricated.
- Overlap with the 3 published cancer editions is allowed (user decision);
  domains are independent selections, not a partition of one repo set.

## Zero-yield repos (informational, 61)

- opencobra/cobrapy
- oncologylab/craftgrn
- prathyvsh/formal-systems-in-biology
- bioFAM/MOFA2
- opencobra/cobratoolbox
- ICB-DCM/pyPESTO
- franciscozorrilla/metaGEM
- YuLab-SMU/enrichplot
- gyorilab/indra
- Murali-group/Beeline
- cafferychen777/ggpicrust2
- saeyslab/multinichenetr
- pysb/pysb
- AMICI-dev/AMICI
- micom-dev/micom
- pybel/pybel
- SysBioChalmers/yeast-GEM
- Future-House/LAB-Bench
- pinellolab/dictys
- scverse/mudata
- copasi/COPASI
- florianhartig/BayesianTools
- saezlab/CollecTRI
- MaayanLab/biojupies
- netZoo/netZooR
- iaconogi/bigSCale2
- saezlab/corneto
- refinery-platform/refinery-platform
- AstraZeneca/onto_merger
- RasmussenLab/MOVE
- netZoo/netZooPy
- SysBioChalmers/GECKO
- igordot/msigdbr
- xcsp3team/pycsp3
- dportik/Biotech-Job-Search-Engine
- PayamDiba/SERGIO
- dynverse/dyngen
- jackbibby1/SCPA
- ZJUFanLab/scRank
- aertslab/arboreto
- GeomScale/dingo
- SciML/CellMLToolkit.jl
- jpquast/protti
- PEtab-dev/PEtab
- aplbrain/grandiso-networkx
- Data2Dynamics/d2d
- opencobra/COBRA.jl
- Vinay0905/Fish-Detection-YOLOv8
- ecell/ecell4_base
- iVis-at-Bilkent/newt
- iVis-at-Bilkent/pathway-mapper
- sbmlteam/libsbml
- cantinilab/Mowgli
- biosustain/shu
- flatironinstitute/inferelator
- ReactionMechanismGenerator/ARC
- klamt-lab/straindesign
- Noble-Lab/HiCFoundation
- LarsonLab/hyperpolarized-mri-toolbox
- SciML/MomentClosure.jl
- bioFAM/mofaflex

## Caveats

- Static validation only; real grading needs an LLM judge key + Docker.
- inline_dockerfile mode skips image build (no Docker daemon needed to publish).
- Provider secrets in upstream diffs were redacted before public release.
