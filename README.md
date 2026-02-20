# GrandR <img src="https://img.shields.io/badge/Version-0.1.0-blue?style=flat-square" alt="Version"/>

> **"Professional bioinformatics with a touch of Grandma’s wisdom."**

`GrandR` (Grandma’s Research Toolkit) is a high-performance R infrastructure designed for clinical bioinformatics and multi-omics research. It transforms the chaotic nature of research into a standardized, audited, and visually consistent industrial-grade workflow.

------------------------------------------------------------------------

## 👵 Why GrandR?

In the fast-paced world of high-impact research (**STTT, NC, Nature**), we don't just need scripts; we need a **Research Operating System**. `GrandR` provides the backbone for your analytical lifecycle:

* 🛡️ **`GR_run_recorder`**: **Audit & Reproduce.** Generates full cryptographic audit trails and HTML reports for every experiment. Never wonder *"How did I get this plot?"* ever again.
* 🏗️ **`GR_scaffold`**: **Standardize & Deploy.** Instant deployment of professional-grade project directory trees. Adheres to the principle of *Convention over Configuration*.
* 📦 **`GR_io_write/read`**: **Vault & Stream.** High-speed Parquet-based data asset management with seamless lazy loading for massive multi-omics datasets.
* 🎨 **`GR_pal_set/get`**: **Orchestrate & Visualize.** Multi-theme global color palettes to ensure perfect visual identity across dozens of complex figures.

------------------------------------------------------------------------

## 🚀 Quick Start

### 1. Installation

```{r setup, include=FALSE}
# Install from GitHub devtools::install_github("fengqlin/GrandR")
library(GrandR)
```

**2.Examples**

```{r setup, include=FALSE}
library(GrandR)
library(tidyverse)
library(patchwork)

# ==============================================================================
# 🏗️ STEP 1: Scaffold a Standard Research Workspace
# ==============================================================================
# Initialize a clean, standardized directory structure for a generic study
GR_scaffold("Simulated_Study_2026", author = "Principal Investigator")


# Note: In a real scenario, you would setwd() and source("init.R")
# setwd("Simulated_Study_2026")
# source("init.R")


# ==============================================================================
# 🎨 STEP 2: Configure Global Visual Identity (Palettes)
# ==============================================================================
# Define isolated color themes for different analysis modules
GR_pal_set(
  Control = "#94a3b8", Treated = "#ef4444", 
  theme_id = "Experimental_Design"
)

GR_pal_set(
  High_Risk = "#991b1b", Low_Risk = "#1e40af", 
  theme_id = "Risk_Profile"
)


# ==============================================================================
# 📦 STEP 3: Data Ingestion into the Vault (IO)
# ==============================================================================
# Create mock multi-omics data (1000 features x 50 samples)
mock_data <- data.frame(
  Sample_ID = paste0("S_", 1:50),
  Group = sample(c("Control", "Treated"), 50, replace = TRUE),
  Biomarker_Alpha = rnorm(50),
  Biomarker_Beta  = rnorm(50)
)

# Ingest data into the high-speed Parquet vault
GR_io_write(mock_data, asset_name = "Discovery_Cohort_V1")


# ==============================================================================
# 🛡️ STEP 4: Record a Standard Analytical Task
# ==============================================================================
# Define a generic analysis function
analyze_biomarker_distribution <- function(asset_name) {
  
  # Pull data from the vault (Smart IO)
  df <- GR_io_read(asset_name)
  
  message("Calculating statistical distributions...")
  
  # Core Plotting logic using GrandR Palettes
  p <- ggplot(df, aes(x = Group, y = Biomarker_Alpha, fill = Group)) +
    geom_boxplot(notch = TRUE, outlier.shape = NA) +
    geom_jitter(width = 0.2, alpha = 0.5) +
    scale_fill_manual(values = GR_pal_get(c("Control", "Treated"), 
                                          theme_id = "Experimental_Design")) +
    theme_classic() +
    labs(title = "Biomarker Alpha Distribution by Group",
         subtitle = paste("Source Asset:", asset_name))
  
  # Return result as a list (Recorder will capture the plot and the data)
  return(list(
    Distribution_Plot = p,
    Summary_Stats = df %>% group_by(Group) %>% summarise(Mean = mean(Biomarker_Alpha))
  ))
}

# Execute with the Research Recorder (Automatic caching and HTML auditing)
final_result <- GR_run_recorder(
  func = analyze_biomarker_distribution,
  asset_name = "Discovery_Cohort_V1",
  note = "Initial_Biomarker_Screen"
)


# ==============================================================================
# 🛰️ STEP 5: Visual Exploration of Assets & History
# ==============================================================================
# At any time, you can invoke these to view your "Research OS" state:

# GR_view_api()      # Explore all standardized function assets
# GR_view_vault()    # Inspect ingested Parquet data assets
# GR_view_indexer()  # View the visual timeline of all research runs
```
