# MIPSA_HSV
HSV peptides and Human Antibodies in MIPSA
Analysis for: **Large-scale antibody reactome profiling identifies herpesvirus–autoantigen associations underlying chronic diseases**.

This repository reproduces the analyses described in the manuscript: cohort seroprevalence, Hu↔HSV GLMs, replication, prediction models, disease associations, and tripartite network plots.

## Directory layout
mipsa-seroprev/
├─ R/
│ ├─ utils_common.R
│ └─ utils_qtl.R
├─ scripts/
│ ├─ figure_disease_counts.R # Fig 1C/1D
│ ├─ virus_seroprev_plots.R # Fig 2A/2B
│ ├─ human_seroprev_ridgeline.R # Fig 2C/2D
│ ├─ build_binary_matrices.R # create binary/log matrices from MIPSA
│ ├─ run_hu_vs_hsv_glm.R # Hu ~ Virus GLMs (+ optional Virus ~ Hu), discovery + replication
│ ├─ collect_annotate_results.R # annotate, BH-FDR, replication join, prevalence
│ ├─ run_disease_association_glm.R # Disease ~ (Virus or Autoantigen) GLMs
│ └─ plots_qtl_panels.R # diamond, circos, manhattan panels F Fig 3
│ └─ plots_qtl_panels.R # diamond, circos, manhattan panels


## Data expectations
- **Viral**: VirSIGHT peptide/protein hits (binary), with UniProt IDs and taxonomic annotations.
- **Human**: HuSIGHT full-length hits (binary), with UniProt and HGNC gene symbol.
- **Phenotypes**: Demographic covariates (Age, Sex/Gender, BMI, Race, Smoking, Alcohol), and disease endpoints (prevalent, incident).
- **Replication cohort**: matching ID space for strict peptide–autoantigen ID matches.

Paths are passed via command-line args; see each script’s `--help` section.

## Repro order (discovery → replication)
1. `scripts/build_binary_matrices.R`
2. `scripts/virus_seroprev_plots.R` and `scripts/human_seroprev_ridgeline.R`
3. `scripts/run_hu_vs_hsv_glm.R` (discovery), then again for replication
4. `scripts/collect_annotate_results.R` (merges discovery + replication, FDR, annotations)
5. `scripts/run_disease_association_glm.R`
6. `scripts/plots_qtl_panels.R` + network plots (you can port your existing network code or use the helpers here)

## Software
R ≥ 4.2 with: `data.table`, `dplyr`, `tidyr`, `ggplot2`, `ggrepel`, `glmnet`, `pROC`, `igraph`, `ggraph`, `scales`, `argparse`, `readr`, `stringr`.

## Citation
Please cite the manuscript when using this code.
