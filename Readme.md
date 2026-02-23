## Vimentin Disassembly is a Structural Prerequisite for Enucleation in iPSC-Derived Erythrocytes: Insights from Avian Erythropoiesis

![R version 4.4.3+](https://img.shields.io/badge/R-4.4.3+-blue.svg)
![Seurat 5.3.0](https://img.shields.io/badge/Seurat-5.3.0-orange.svg)
![MIT License](https://img.shields.io/badge/License-MIT-green.svg)

##Project Overview
This repository contains the complete analytical pipeline for the study: **"Vimentin Disassembly is a Structural Prerequisite for Enucleation in iPSC-Derived Erythrocytes: Insights from Avian Erythropoiesis"** (Jahejo et al., 2026).

##Multi-Environment Reproducibility
Due to updates in the Seurat integration ecosystem, this project utilizes two distinct computational environments:
Workflow Stage	Component	Software Requirement
Legacy Integration	Script 01 (Phase 1A)	R v4.1.3 + Seurat v4.1.3
Main Analysis	Scripts 01 (Phase 1B), 02, 03, 04	R v4.4.3 + Seurat v5.3.0
Recommended Execution Path
To avoid environment conflicts, users are encouraged to skip Phase 1A and begin directly with the main analysis (Phase 1B) using the pre-integrated data:
Download GSE315210_BMscRNA_integrated.rdata.gz from GEO.
Decompress and rename it to BMscRNA_integrated.RData.
Place it in ./Processed_Objects/.
Run all scripts using the R v4.4.3 / Seurat v5 environment.

##Directory Structure

Avian-Erythroid-Atlas/
├── 01_Avian_Erythroid_Atlas_BoneMarrow.Rmd        # Script 1: Atlas Construction
├── 02_Integration_Avian_Erythroid_Atlas_PB.Rmd    # Script 2: Blood-Marrow Integration
├── 03_Validation_of_Avian_Erythroid_Stages.Rmd    # Script 3: Bulk RNA-seq Validation
├── 04_Comparative_Human_vs_Avian.Rmd             # Script 4: Cross-species Analysis
├── Raw_Data/                                      # Input Data
│   ├── Primary_Avian_Marrow/                      # GEO: GSE315210
│   │   ├── BM_1/                                  # 10X Replicate 1
│   │   └── BM_2/                                  # 10X Replicate 2
│   └── Public_Reference_Data/
│       ├── Human_Atlas_HscRNA/                    # GEO: GSE253355
│       └── Maxwell_2024_PBscRNA/
│           ├── PBscRNA_1/                         # Blood Replicate 1
│           ├── PBscRNA_2/                         # Blood Replicate 2
│           ├── PBscRNA_3/                         # Blood Replicate 3
│           └── PBscRNA_4/                         # Blood Replicate 4
│       └── Pavani_2024/                           # iPSC Dataset (GSE242101)
├── Processed_Objects/                             # Generated .RData and .rds files
├── Results/                                       # Primary Figures
│   └── Result_Supporting_Files/                  # Diagnostic and QC plots
├── Environment/                                   # renv.lock and session_info.txt
├── External_Data_File/                            # Ortholog mappings & Bulk CSVs
├── External_Data_Guide.md                         # Detailed data source documentation
└── Readme.md                                      # This file

##Data Access
Primary Avian Marrow: Download from NCBI GEO GSE315210.
Human Reference Atlas: Download processed Seurat object from NCBI GEO GSE253355.
Avian Peripheral Blood: Download 10x outputs from the maxwelma/exjobb GitHub repository.
Bulk Validation:
T2EC Progenitors: Richard et al. 2016 (Provided as re-annotated CSV in External_Data_File/).
Polarized Erythrocytes: PRJNA305527 & PRJNA445563 (Provided as CSV in External_Data_File/).
Human iPSC Erythroblasts: Download processed Seurat object from NCBI GEO GSE242101.

##Setup & Analysis Workflow
1. Environment Setup (Main Analysis)
We use renv to manage dependencies for the Seurat v5 environment. To restore:
install.packages("renv")
renv::restore() # Run this in the project root

2. Script Details
[01] Bone Marrow Atlas: Handles SCTransform, cell-cycle regression, and annotation of the marrow lineage. (Phase 1A: Seurat v4; Phase 1B: Seurat v5).
[02] Blood Integration: Integrates mature circulating erythrocytes and performs metabolic pathway scoring (scMetabolism).
[03] Bulk Validation: Correlates single-cell clusters with established bulk RNA-seq models to verify developmental stage identities.
[04] Comparative Analysis: The core cross-species comparison. Features include Monocle3 trajectory modeling, VIPER/DoRothEA TF activity profiling, and CellChat niche signaling.

##Citation
If you use this code or the Avian Erythroid Atlas, please cite:
Jahejo et al. (2026). Vimentin Disassembly is a Structural Prerequisite for Enucleation in iPSC-Derived Erythrocytes: Insights from Avian Erythropoiesis (In Review).

##License & Contact
Distributed under the MIT License. For technical queries, please open an issue in this repository or contact the author Ali Raza Jahejo at arjahejo@gmail.com.
