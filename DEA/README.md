# Differential Expression Analysis

Before applying the machine learning algorithms, here we first did a differential exression analysis for feature selection using this TCGA RNA-seq dataset.

|Data               | File             |
|-------------------|------------------|
|Tximport object    |SalmonTXI_TCGA.rds|
|Patient information| tcga-cdr.csv     |
|Sample information | sample.info.tsv  |

| Scripts         |Step |
|-----------------|-----|
|data.process.Rmd |1,2,3|
|DE1.Rmd          |4-1  |
|allGenes.DE1.Rmd |4-2  |
|Single.DE.Rmd    |4-3  |
|GSEA.Rmd         |5    |


### Main steps

#### 1. Filtering
- Discard patients with multiple metastatic sites;
- Keep primary tumor samples only.
 
#### 2. Split the dataset according to biotypes
- Use biomaRt package to extract protein-coding genes;
- Confirmed that the tximport object was generated using ENSEMBL v75 hg19 annnotation GTF file (tximport is to summarize abundance from transcript level to gene level).
 
#### 3. Generate gene-level counts-from-abundance
- Scale the count matrix for afterward limma-voom implementation

#### 4. Limma-voom 
##### 4-1. For protein-coding genes pancancer subset
##### 4-2. For all genes pancancer set
##### 4-3. Implement limma-voom in cancer types with more than 10 metastasis samples for coding gene subsets
- Fitler out samples with large proportion of lowly-expressed genes (outliers);
- Remove lowly-expressed genes using functions in DESeq2 & edgeR;
- Normalize the counts using TMM method;
- Voom and limma:
  - design1: ~ Metastasis
  - design2: ~ Metastasis + type (adding the confounding factor cancer type)
- Draw boxplots with top several DEGs for each cancer type and heatmap using 30 DEGs (q-vals and logFC threshold see the file).

#### 5. Functional enrichment analysis
 - Conducted pre-ranked GSEA using gene lists ranked by the t-statistics from the results of DE analysis;
 - Evaluation: 

---
### Conclusions:



