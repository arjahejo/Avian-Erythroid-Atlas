# External Data Guide

This document describes the acquisition, processing rationale, and directory organization of the public datasets and orthology references used to analyze avian nuclear retention and human enucleation.

---

## 1. Avian Peripheral Blood scRNA-seq (PBscRNA)
*   **Source:** Maxwell et al. (2024), *BMC Genomics* (DOI: 10.1186/s12864-024-10044-4).
*   **Rationale:** Integrated to resolve the terminal stage of erythropoiesis. While marrow-derived data (BMscRNA) captures progenitors through blasts, it lacks fully mature erythrocytes which reside in circulation.
*   **Data Acquisition:** Download standard 10x Genomics outputs (matrix.mtx, features.tsv, and barcodes.tsv) for biological replicates (Sample 1-4) from the public repository: [maxwelma/exjobb](https://github.com/maxwelma/exjobb).
*   **Placement:** Decompress and place in `./Raw_Data/Public_Reference_Data/Maxwell_2024_PBscRNA/`.

## 2. Avian Erythroid Progenitor Bulk RNA-seq (T2EC)
*   **Source:** Richard et al. (2016), *PLOS Biology* (DOI: 10.1371/journal.pbio.1002585) File:matrix_2793.txt (https://osf.io/k2q5b/files/fsgkb).
*   **Processing:** Legacy Ensembl v4 identifiers were re-annotated by aligning transcript sequences against Ensembl v7 using BLASTn to transfer official Gene Symbols.
*   **Validation:** Used to correlate early single-cell clusters with LM1 (self-renewal) and DM17 (differentiation) bulk profiles.
*   **Placement:** The re-annotated file need to place at `./External_Data_File/Richard2016_Bulk_T2EC.csv`.

## 3. Polarized Erythrocyte Bulk RNA-seq (Immature vs. Mature)
*   **Source:** 
    *   Immature Erythrocytes: NCBI SRA [SRR2983618](https://www.ncbi.nlm.nih.gov/sra/SRR2983618)
    *   Mature Erythrocytes: NCBI SRA [SRR6893554](https://www.ncbi.nlm.nih.gov/sra/SRR6893554)
*   **Processing:** Raw FASTQ files were quantified using Salmon (quasi-mapping) and summarized to gene-level counts via the `tximport` R package.
*   **Validation:** Used to benchmark terminal single-cell clusters against respective bulk counterparts.
*   **Placement:** Processed gene-level counts need to place at `./External_Data_File/Immature_Ery.csv` and `./External_Data_File/Mature_Ery.csv`.

## 4. Human Bone Marrow Reference Atlas (HscRNA)
*   **Source:** Bandyopadhyay et al. (2024), *Cell* (DOI: 10.1016/j.cell.2024.04.013).
*   **Rationale:** Provides a high-resolution benchmark for mammalian enucleation to compare against avian nuclear retention. 
*   **Data Acquisition:** Download the processed Seurat object `GSE253355_Normal_Bone_Marrow_Atlas_Seurat_SB_v2.rds.gz` from [NCBI GEO GSE253355](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE253355).
*   **Placement:** Decompress and place in `./Raw_Data/Public_Reference_Data/Human_Atlas_HscRNA/GSE253355.rds`.

## 5. Orthology Reference Mapping
The following reference files enable cross-species transcriptomic alignment of chicken and human data on a shared human gene namespace (Ensembl release 111).

### biomart_chicken_human_raw.txt
*   **Methodology:** Manual export from Ensembl BioMart (Chicken genes dataset) with human orthologue gene ID, gene name, homology type and orthology confidence. Never edited by hand.
*   **Purpose:** Unmodified source for both ortholog tables below (Script 4C).
*   **Placement:** `./External_Data_File/biomart_chicken_human_raw.txt`.

### orthologs_ALL_ensembl111.tsv
*   **Methodology:** Generated in code from the raw export; keeps all chicken genes with a human ortholog (all homology types).
*   **Purpose:** Gene lookups without a one-to-one requirement, e.g. mapping human SRF (VIPER-inferred activity) to its chicken ortholog mRNA trajectory.
*   **Placement:** `./External_Data_File/orthologs_ALL_ensembl111.tsv`.

### orthologs_one2one_ensembl111.tsv
*   **Methodology:** Restricted to one-to-one orthologs; human symbols shared by more than one chicken gene are removed.
*   **Purpose:** Maps chicken genes to human symbols for the Spearman correlation, unified cross-species UMAP and stage-matched analyses.
*   **Placement:** `./External_Data_File/orthologs_one2one_ensembl111.tsv`.

**Note:** For large datasets (>100MB) such as the Human RDS or primary Avian matrix files, users must download them directly from the provided links as they are not hosted on GitHub due to size limitations.