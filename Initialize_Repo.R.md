################################################################################
# Script: Initialize_Repo.R
# Purpose: Creates the required folder structure and adds .gitkeep files
#          to ensure empty directories are tracked by Git/GitHub.
################################################################################

# 1. Define all folders required by the project
folders_to_keep <- c(
  "Raw_Data/Primary_Avian_Marrow/BM_1",
  "Raw_Data/Primary_Avian_Marrow/BM_2",
  "Raw_Data/Public_Reference_Data/Human_Atlas_HscRNA",
  "Raw_Data/Public_Reference_Data/Maxwell_2024_PBscRNA/PBscRNA_1",
  "Raw_Data/Public_Reference_Data/Maxwell_2024_PBscRNA/PBscRNA_2",
  "Raw_Data/Public_Reference_Data/Maxwell_2024_PBscRNA/PBscRNA_3",
  "Raw_Data/Public_Reference_Data/Maxwell_2024_PBscRNA/PBscRNA_4",
  "Raw_Data/Public_Reference_Data/Pavani_2024",
  "Processed_Objects",
  "Results",
  "Results/Result_Supporting_Files",
  "External_Data_File",
  "Environment"
)

# 2. Loop through and create folders + .gitkeep files
cat("Starting repository initialization...\n")

for (f in folders_to_keep) {
  # Create directory if it doesn't exist
  if (!dir.exists(f)) {
    dir.create(f, recursive = TRUE)
    cat("Created folder:", f, "\n")
  }
  
  # Create the .gitkeep file inside the folder
  keep_file <- file.path(f, ".gitkeep")
  if (!file.exists(keep_file)) {
    file.create(keep_file)
    cat("Added .gitkeep to:", f, "\n")
  }
}

cat("\n✅ Success: All directories are verified and ready for GitHub.\n")