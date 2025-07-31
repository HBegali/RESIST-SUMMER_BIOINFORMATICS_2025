# Introduction to Accessing MHH-HPC

## 🧠 Background

**High-Performance Computing (HPC)** refers to the use of supercomputers and parallel processing techniques to solve complex computational problems at high speeds. At MHH, the HPC environment supports large-scale data analysis, modeling, and bioinformatics workflows.

---

## 📊 HPC System Overview

The diagram below shows how the HPC system is structured, including login nodes, compute nodes, and shared storage:

![assets/fig1.png](assets/fig1.png)
<p align="center">
  <img src="assets/fig1.png" alt="Pipeline Diagram" width="700" />
</p>

---

## 📁 Directory Structure on HPC

The HPC system organizes user files under a shared project directory. This structure ensures a clean and manageable workspace for each user.

![HPC Diagram](assets/fig1.png)




--

## 💻 Accessing HPC from Your Local Machine

You can transfer files between your local computer and the HPC system using the network path below:

### 📂 Steps to Access Shared Folder:
1. Open **File Explorer** on your Windows computer.
2. In the address bar, type: ``` \\essces ```
3. Press **Enter**.
4. Navigate through the following folders: - `project` - `summerinformatics` - `2025_Users`
5. Create your personal folder using your name (e.g., `Hanan`, `Erik`, etc.).
<p align="center">
  <img src="assets/fig1.png" alt="Pipeline Diagram" width="700" />
</p>


 ## 🧪 Activating Compute Node & Launching RStudio To use computing power (cores, memory) for analysis,
  you'll need to **activate a compute node** and launch **RStudio** via the web interface.
  ### 📝 Steps to Start an R Session on HPC ####
  🔗 Step 1: Login to the HPC Web Portal
  1. Open your browser and go to: ``` https://leineood.mh-hannover.local/ ```
  2. Enter your **MHH username and password** (same as your hospital/work PC login). ![Login Screen](assets/fig5.png) ---
  #### 🧠 Step 2: Launch RStudio Session
   1. Click on: - **CPU – Software** - Then select **RStudio - Advanced** ![RStudio Selection](assets/fig6.png) ---
   #### ⚙️ Step 3: Configure Your Job Settings On the job submission page, fill in the following details:
   - **Container Path**: ``` /hpc/project/summerinformatics/environments/summerinformatics_RStudio.sif ```
    - **Password**: Choose a temporary session password, e.g., `123`
    - **Cores**: `4`
    - **Memory (MB)**: `16000`
    - **Job Time (hours)**: `8`
    - **Reservation**: `XXX` *(if applicable; otherwise leave it blank)* Leave all other fields as default.
    Then click **Launch** to start your RStudio session. ![Job Submission Example](assets/fig7.png)












This pipeline processes `.fcs` files, performs clustering, subsampling, visualization, statistical testing, and generates publication-ready plots to assess immune profiles in **HDV patients** and **Healthy Controls**.

## Pipeline Diagram

<p align="center">
  <img src="assets/FrameWork_HB_20250725.png" alt="Pipeline Diagram" width="700" />
</p>

## 🔬 Methodology

### 1. Data Preprocessing & Marker Harmonization
- Import `.fcs` using `flowCore::read.flowSet()`
- Extract metadata, clean marker names
- Apply biexponential transformation on selected markers

### 2. Data Transformation & Clustering
- Quantile normalization (`matrixStats`)
- Clustering using `FlowSOM` and `ConsensusClusterPlus`
- Parallel computation using `doParallel` + `foreach`

### 3. Subsampling & Deduplication
- Random sampling (100,000–300,000 cells per group)
- Ensure balanced sample sizes across conditions

### 4. Dimensionality Reduction & Visualization
- Use `Rtsne` for t-SNE plots
- Visualize clusters using `ggplot2`, `scattermore`, `ggpointdensity`, etc.

### 5. Cluster Quantification & Marker Analysis
- Aggregate marker expression per cluster
- Visualize trends across clinical groups/timepoints

### 6. Statistical Testing
- Wilcoxon test, Kruskal–Wallis + Dunn’s post hoc
- Adjust p-values using Benjamini–Hochberg (FDR)
- Annotate plots with `rstatix`, `ggsignif`

### 7. Heatmap Generation
- Cluster-level marker expression heatmaps using `pheatmap`
- Stratified by group and timepoint

## 🧪 Experimental Groups

- Healthy Controls (HC)
- Baseline HCV (BLHCV)
- HDV Subgroups:
  - Baseline: BLResponder, BLNonResponder
  - Week 3: W3Responder, W3NonResponder
  - Week 48: W48Responder, W48NonResponder

## 🛠️ Environment

All analyses were performed on a high-performance computing (HPC) cluster at Hannover Medical School (MHH):

- **R version**: 4.3.1
- **Resources**: 400 GB RAM, 4 CPU cores/node
- **Data formats**: `.fcs`, `.rds`, `.csv`

### 📦 Key Packages

| Task | Packages |
|------|----------|
| Import & transform | `flowCore`, `FlowSOM` |
| Clustering & normalization | `ConsensusClusterPlus`, `matrixStats`, `doParallel`, `foreach` |
| Dimensionality reduction | `Rtsne` |
| Data wrangling | `dplyr`, `tidyr`, `stringr`, `purrr`, `tibble`, `forcats` |
| Plotting | `ggplot2`, `ggrepel`, `scattermore`, `ggrastr`, `ggpointdensity`, `ggridges`, `cowplot`, `patchwork` |
| Stats | `rstatix`, `ggsignif`, `stats` |
| Heatmaps | `pheatmap` |

## 📘 How to Cite

If you use this pipeline or any part of it in your research, please cite the relevant R packages listed above and acknowledge this repository.

---

## 🧠 Contributors

- **Project Lead:** BDAG members — Prof. Drs. Daniel Depledge, Marco Galardini, Chris Lauber, Dr. med. Helenie Kefalakes  
- **Bioinformatics Analysis:** Hanan Begali  
- **Wet Lab Team:** AG_Kefalakes: PhD student Reem Hoblos
- **Contact:** hananalbegali@gmail.com

---

## 📌 License

This repository is made available for academic use only. Please refer to individual package licenses for usage details.

---

---

## 📁 Repository Structure
