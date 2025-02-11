> ``

## **This is a ReadMe file for the project "Single cell analyses reveal functional heterogeneity within an exhausted CD8+ TIL population that is correlated with response to checkpoint therapy in melanoma."**##

---

# Single cell analyses reveal functional heterogeneity within an exhausted CD8+ TIL population that is correlated with response to checkpoint therapy in melanoma

### Running Title: TIL heterogeneity associated with ICI response in melanoma

Authors: Kelly M. Mahuron 1,2+, Osmaan Shahid 3,4+, Prachi Sao 5,+, Clinton Wu 6,+, Alexandra M. Haugh 7,8, Laura A Huppert 7,8,  Lauren S. Levine 7,8, Margaret M. Lowe 9, Michael Alvarado 1, Markee Micu 7, Katy K. Tsai 7,8, Melissa Chow 8, Meromit Singer 3,10,11,12, Jason M. Schenkel 5,13,14, Arlene H. Sharpe 3,4,10, Michael D. Rosenblum 9*, Kristen E. Pauken 5*, Adil I. Daud 7*

 _+ co-first authors

 _* corresponding authors

### Affiliations

1 Department of Surgery, University of California San Francisco, San Francisco, CA, USA
2 Department of Surgery, City of Hope National Medical Center, Duarte, CA, USA
3 Department of Immunology, Blavatnik Institute, Harvard Medical School, Boston, MA, USA
4 Gene Lay Institute of Immunology and Inflammation at Brigham and Women’s Hospital, Massachusetts General Hospital and Harvard Medical School
5 Department of Immunology, The University of Texas MD Anderson Cancer Center, Houston, TX, USA.
6 Department of Medicine, University of Arizona Tucson, Tucson, AZ, USA
7 Department of Medicine, University of California San Francisco, San Francisco, CA, USA
8 Helen Diller Family Comprehensive Cancer Center, University of California San Francisco, San Francisco, CA, USA
9 Department of Dermatology, University of California San Francisco, San Francisco, CA, USA
10 Broad Institute of MIT and Harvard, Cambridge, MA, USA
11 Department of Data Sciences, Dana-Farber Cancer Institute, Boston, MA, USA
12 Present address: Guardant Health, Palo Alto, CA, USA
13 Department of Translational Molecular Pathology, The University of Texas MD Anderson Cancer Center, Houston, TX 77030, USA.
14 Department of Laboratory Medicine, The University of Texas MD Anderson Cancer Center, Houston, TX 77030, USA.

**For Code-Related Queries:**
Prachi Sao
Email Address: psao@mdanderson.org

**Find the paper here!**
"Add the link to the paper"

---

### The scRNA-seq and bulk RNA-seq analyses presented in the manuscript were performed with open-source algorithms as described in Methods. Further details regarding the code used for this study can be found here in this repository, with the relevant references included.

Github Author: "Prachi Sao"
Date: "2021-06-30"
Email Address: psao@mdanderson.org
Organization: PAUKEN LAB, MD ANDERSON CANCER CENTER"

---

### Data

The integrated Seurat object is deposited to GEO " add geo id"

Excel File for gene set enrichment analysis is given as supplementary file S4 "TableS4_SupplementGeneSigs.xlsx"

The published datasets can be found at the following GEO repository:

The bulk RNA seq data used in this study is publicly available on the GEO database (accession number GSE147620). Single cell sequencing and TCR-sequencing data from this paper can be found at accession numbers GSE148190 and GSE159251. The processed data object can be found at GSE148190. The validation dataset was accessed from GEO accession number GSE120575.

### Description

To analyze CD8+ T cell data, we started by loading the pre-processed data from an RDS file (GEO id for integrated object).
Using DimPlot, we create a scatter plot of cells based on their principal components to visualize clusters.
and VizDimLoadings to understand which genes contribute most to the first two principal components. We then
remove T-cell receptor (TCR) genes, which start with “TRA”, “TRB”, “TRD”, or “TRG”. Next, We use VlnPlot to
Create violin plots that visualize the distribution of RNA features and counts. We filter cells based on the
number of detected features and mitochondrial gene percentage to ensure quality.
split the RNA data by sample for further analysis. The gene expression data is normalized to make it
comparable across cells, and genes showing high variability are identified for downstream analysis.
The data is scaled to have a mean of 0 and variance of 1, which is necessary for PCA.
Principal Component Analysis (PCA) is performed to reduce dimensionality and identify major sources of variation.
Data from different samples is integrated using Canonical Correlation Analysis (CCA) to correct for batch effects.
and the RNA layers are rejoined after integration.
The basic Seurat workflow was rerun on the integrated data, and clusters were identified using the FindClusters function.
The data was visualized using UMAP, and cluster identities were assigned based on the integrated data.
Differential expression analysis was performed to identify genes that are differentially expressed between clusters.
The WilcoxAUC function was used to identify genes that are differentially expressed between clusters.
The results were visualized using a violin plot and a box plot.
Topic modelling was performed using Latent Dirichlet Allocation (LDA) on the object and saves the resulting LDA model to an RDS
The validation dataset was taken from a 2018 study published in Cell. Sade-Feldman et al. examined immune cells from melanoma patients before and after immune checkpoint blockade therapy.
The dataset GSE120575 comprises CD45+ single cells from 48 melanoma tumor biopsies, taken before and after checkpoint inhibitor treatment. This data, sequenced using the Smart-seq2 protocol, includes metadata on therapy response (Responder vs. Non-responder) under the same GEO identifier.

### Make folder as used in all the codes

Make a folder in the working directory and name it as "project" and put all the data files in this folder.
The project folder will have the following files:

1. Raw_data
2. Results
   files
   plots
   RDS
3. Scripts

### R scripts

### Create a new directory named "project" in the working directory

`if (!dir.exists("project")) { dir.create("project") }`

### Create subdirectories within the "project" directory

`subdirs <- c("Raw_data", "Results/files", "Results/plots", "Results/RDS", "Scripts") for (subdir in subdirs) { dir.create(file.path("project", subdir), recursive = TRUE) }`
Download all the data to the Raw_data folder for further analysis.

### Package Installation

`install.packages("BiocManager")`

`BiocManager::install(c("DESeq2", "Seurat", "Azimuth", "presto", "dplyr", "cowplot", "viridis", "gridExtra", "data.table", "tibble", "Matrix", "ggplot2", "patchwork", "grid", "RColorBrewer", "clustree", "pheatmap", "msigdbr", "purrr", "clusterProfiler", "scater", "MatrixGenerics", "tidyverse", "ComplexHeatmap", "circlize", "scCustomize", "qs", "dittoSeq", "ggpubr", "reshape2", "fgsea", "useful", "readxl", "msigdbr"))`

Version of Packages: sessionInfo.txt

### Code References

The code used here follows the standard Seurat workflow as given in the vignette **https://satijalab.org/seurat/articles/integration_introduction.html**

For topic modeling, the TITAN package is used. TITAN (Topic Inference of Transcriptionally Associated Networks) is an R package that runs topic modeling on scRNA-seq data.
**https://github.com/ohsu-cedar-comp-hub/TITAN.git**
Current Version of TITAN located here: **https://github.com/ohsu-cedar-comp-hub/TITAN**

Some of the codes are adopted from previous work of authors:

Blood_Tumor_Code is the GitHub repository that holds the code for the paper published at the Journal of Experimental Medicine:
"Single-cell analyses identify circulating anti-tumor CD8 T cells and markers for their enrichment."
**https://github.com/MSingerLab/Blood_Tumor_Code.git**

For Validation Data
following Reference was used

**https://github.com/KlugerLab/DAseq-paper/blob/master/DAseq_melanoma.R**
**https://carmonalab.github.io/ProjecTILs_CaseStudies/SadeFeldman_ortho.html**
