# Comparative single-cell analysis of human and chicken erythropoiesis highlights nuclear retention and early avian erythroid immunity

![R](https://img.shields.io/badge/R-4.4.3+-blue) ![Seurat](https://img.shields.io/badge/Seurat-5.3.0-green) ![License](https://img.shields.io/badge/License-MIT-yellow)

## Project Overview
This repository contains the complete analytical pipeline for the study: "Comparative single-cell analysis of human and chicken erythropoiesis highlights nuclear retention and early avian erythroid immunity" (Jahejo et al., 2026).

## Multi-Environment Reproducibility
Due to updates in the Seurat integration ecosystem, this project uses two computational environments:

| Workflow Stage | Component | Software Requirement |
|---|---|---|
| Legacy Integration | Script 01 (Phase 1A) | R v4.1.3 + Seurat v4.1.3 |
| Main Analysis | Scripts 01 (Phase 1B), 02, 03, 04 | R v4.4.3 + Seurat v5.3.0 |

### Recommended Execution Path
To avoid environment conflicts, skip Phase 1A and begin directly with the main analysis (Phase 1B) using the pre-integrated data:

1. Download `GSE315210_BMscRNA_integrated.rdata.gz` from GEO.
2. Decompress and rename it to `BMscRNA_integrated.RData`.
3. Place it in `./Processed_Objects/`.
4. Run all scripts using the R v4.4.3 / Seurat v5 environment.

## Directory Structure
```text
Avian-Erythroid-Atlas/
├── 01_Avian_Erythroid_Atlas_BoneMarrow                  # Script 1: Atlas Construction
├── 02_Integration_Avian_Erythroid_Atlas_PeripheralBlood # Script 2: Blood-Marrow Integration
├── 03_Validation_of_Avian_Erythroid_Stages              # Script 3: Bulk RNA-seq Validation
├── 04_Comparative_Nuclear_Fate_Regulation_Immunity      # Script 4: Cross-species Analysis
├── Raw_Data/                                            # Input Data
│   ├── Primary_Avian_Marrow/                            # GEO: GSE315210
│   │   ├── BM_1/                                        # 10X Replicate 1
│   │   └── BM_2/                                        # 10X Replicate 2
│   └── Public_Reference_Data/
│       ├── Human_Atlas_HscRNA/                          # GEO: GSE253355
│       └── Maxwell_2024_PBscRNA/
│           ├── PBscRNA_1/                               # Blood Replicate 1
│           ├── PBscRNA_2/                               # Blood Replicate 2
│           ├── PBscRNA_3/                               # Blood Replicate 3
│           └── PBscRNA_4/                               # Blood Replicate 4
├── Processed_Objects/                                   # Generated .RData and .rds files
├── Results/                                             # Primary Figures & Tables
│   └── Result_Supporting_Files/                         # Diagnostic and QC plots
├── Environment/                                         # renv.lock and session_info.txt
├── External_Data_File/                                  # Ortholog mappings & Bulk CSVs
├── External_Data_Guide.md                               # Detailed data source documentation
└── Readme.md                                            # This file
```

## Data Access
- **Primary Avian Marrow:** NCBI GEO [GSE315210](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE315210).
- **Human Reference Atlas:** processed Seurat object from NCBI GEO [GSE253355](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE253355).
- **Avian Peripheral Blood:** 10x outputs from the [maxwelma/exjobb](https://github.com/maxwelma/exjobb) GitHub repository.
- **Bulk Validation:**
  - T2EC progenitors: Richard et al. 2016 (provided as re-annotated CSV in `External_Data_File/`).
  - Polarized erythrocytes: PRJNA305527 & PRJNA445563 (provided as CSV in `External_Data_File/`).
- **Orthology files:** Ensembl release 111 (see `External_Data_Guide.md`).

## Setup & Analysis Workflow

### Environment Setup (Main Analysis)
We use `renv` to manage dependencies for the Seurat v5 environment. To restore, run this in the project root:
```r
install.packages("renv")
renv::restore()
```

### Script Details
- **[01] Bone Marrow Atlas:** SCTransform, cell-cycle regression and annotation of the marrow lineage (Phase 1A: Seurat v4; Phase 1B: Seurat v5).
- **[02] Blood Integration:** integrates mature circulating erythrocytes and performs metabolic pathway scoring (scMetabolism).
- **[03] Bulk Validation:** correlates single-cell clusters with established bulk RNA-seq models to verify developmental stage identities.
- **[04] Comparative Analysis:** the core cross-species comparison, including Monocle3 trajectory modeling, VIPER/DoRothEA TF activity profiling and CellChat niche signaling.

## Citation
If you use this code or the Avian Erythroid Atlas, please cite:
Jahejo et al. (2026). *Comparative single-cell analysis of human and chicken erythropoiesis highlights nuclear retention and early avian erythroid immunity* (In Review).

## License & Contact
Distributed under the MIT License. For technical queries, please open an issue in this repository or contact Ali Raza Jahejo at arjahejo@gmail.com.
