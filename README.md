# HackBio_StageTwo
# **README.md**

# **Single-Cell RNA-seq Analysis — HackBio Internship (Stage Two)**

**Author:** *Joy Abiodun*
**Team:** *Glycine*
**Stage:** *Two — Clear Evidence-Driven Answers*

---

# ** Project Overview**

This repository contains my complete single-cell RNA-seq analysis for the **HackBio Internship Stage Two Single-Cell RNA-seq task**.
The aim of this project was to analyze a provided `.h5ad` file, identify immune cell types, determine whether the sample originates from bone marrow, and evaluate if the patient shows signs of infection or inflammation.

The workflow is entirely reproducible, uses standard computational biology methods, and follows the expected Scanpy pipeline used across modern scRNA-seq analyses.

---

# ** Biological Questions Addressed**

This project answers four key questions:

1. **Which cell types are present in the dataset?**
2. **What biological functions do these cells perform?**
3. **Does the dataset truly come from bone marrow?**
4. **Does the abundance of cell types suggest a healthy or infected individual?**

---

# ** Key Findings**

## **Identified Cell Types (with relative abundance)**

* Nuocytes — **32.6%**
* NK cells — **23.9%**
* γδ T cells — **14.3%**
* Neutrophils — **8.3%**
* Naive B cells — **7.3%**
* Plasma cells — **5.5%**
* Monocytes — **5.4%**
* Platelets — **1.8%**
* Thymocyte-like cells — **0.8%**

These were determined using:

* Leiden clustering
* PanglaoDB canonical markers
* Decoupler’s ULM scoring
* Marker gene matrixplots and tracksplots

---

## **Biological Interpretation (Summary)**

* **Nuocytes:** ILC2-like cells producing type-2 cytokines (IL-4/5/13).
* **NK cells:** Cytotoxic innate lymphocytes targeting infected or stressed cells.
* **γδ T cells:** Rapid responders recognizing non-classical antigens.
* **Neutrophils:** Primary antibacterial responders.
* **Naive B cells:** Antigen-inexperienced B lineage precursors.
* **Plasma cells:** High-rate antibody-producing effectors.
* **Monocytes:** Circulating precursors to macrophages and dendritic cells.
* **Platelets:** Megakaryocyte-derived clotting components.
* **Thymocyte-like cells:** Likely annotation spillover, not true thymic tissue.

---

## **Is the tissue bone marrow?**

**No.**

Evidence clearly suggests that:

* Classical bone marrow populations (HSCs, CMPs, MEPs, erythroid precursors, early megakaryocytes) are *missing*.
* Nuocytes and NK cells are far too abundant for marrow.
* Neutrophils do not appear in the typical maturation gradient found in marrow.
* Thymocyte-like cells suggest annotation spillover.

The dataset appears to be **PBMC-like or enriched immune tissue**, not bone marrow.

---

## **Is the patient infected?**

**No strong signs of infection.**

* Neutrophils (~8%) and monocytes (~5%) are too low for acute infection.
* No activated transcriptional programs detected.
* NK and γδ T-cell enrichment could be due to technical sorting, not biological response.

The immune system appears **non-inflamed**.

---

# ** Directory Structure**

```
project/
│
├── notebooks/
│   └── Stage2_code.ipynb       # Full analysis notebook (your exact workflow)
│
├── data/
│   └── bone_marrow.h5ad        # Input dataset (downloaded inside notebook)
│
├── results/
│   ├── UMAP_plots/             # All UMAP figures
│   ├── matrixplots/            # Marker validation plots
│   ├── violin_plots/           # QC violin plots
│   └── celltype_distribution.csv
│
└── README.md                   # This documentation file
```

---

# ** Software Dependencies (Exact Versions)**

```
Python 3.10
scanpy==1.10
anndata==0.10
decoupler==1.6
celltypist==1.6
scrublet==0.2.3
pandas==2.2
numpy==1.26
scipy==1.11
matplotlib==3.8
seaborn==0.13
igraph==0.11
fa2-modified==0.3.5
crc32c==2.4
```

To install everything:

```bash
pip install scanpy anndata decoupler celltypist igraph fa2-modified crc32c scrublet pandas numpy scipy matplotlib seaborn
```

---

# ** 7. How to Run the Notebook**

The notebook installs all dependencies *inside the notebook itself*, downloads the dataset with `wget`, and runs end-to-end without requiring any external steps.

### ** Option A — Run on Google Colab (recommended)**

1. Upload **Stage2_code.ipynb**
2. Run all cells **sequentially** (top to bottom)
3. The notebook will automatically:

   * Install all required packages:

     ```python
     !pip install scanpy anndata decoupler celltypist igraph fa2-modified crc32c
     ```
   * Download the dataset using:

     ```python
     !wget -O bone_marrow.h5ad https://github.com/josoga2/sc/raw/refs/heads/main/bone_marrow.h5ad
     ```
   * Perform QC, clustering, UMAP, annotation, marker validation, and final interpretation
4. All plots will render automatically in the output
5. You can save any figure using the standard Google Colab "Download" option

### ** Option B — Run Locally (Jupyter Notebook)**

1. Install Python 3.10
2. Install the dependencies manually using the `pip install` command above
3. Download the dataset manually or allow the notebook to download it
4. Open the notebook:

```bash
jupyter notebook Stage2_code.ipynb
```

5. Run every cell in order

The notebook is fully reproducible because the code:

* Installs all dependencies internally
* Downloads the dataset internally
* Executes the full analysis pipeline without external configuration

---

# **📌 Summary of What This Notebook Produces**

After running the notebook, you will obtain:

* **UMAP plots** for clusters, QC metrics, and annotated cell types
* **Leiden cluster visualizations** at three different resolutions
* **Decoupler ULM signature heatmaps**
* **Matrixplots & tracksplots** for classical markers
* **Final immune cell–type distribution table**
* **Full biological interpretation**
* **Bone marrow assessment**
* **Infection/inflammation assessment**

Everything is generated automatically by following the exact workflow.

---




