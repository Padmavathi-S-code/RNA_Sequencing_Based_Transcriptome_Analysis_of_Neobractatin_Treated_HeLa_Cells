# 00. Project Overview

## 1. Project Title

**RNA-Sequencing Based Transcriptome Analysis of Neobractatin-Treated HeLa Cells**

---

## 2. Project Summary

This project investigates how the natural compound **Neobractatin (NBT)** affects gene expression in **HeLa cells** using publicly available **bulk RNA-seq** data.

The analysis compares:

- **DMSO-treated HeLa cells** — control
- **Neobractatin-treated HeLa cells** — treatment

The goal is to identify genes and biological pathways whose expression changes following Neobractatin treatment.

The project follows a complete bulk RNA-seq workflow, beginning with raw sequencing reads and progressing through quality control, read trimming, genome alignment, gene-level quantification, differential expression analysis, and functional enrichment.

---

## 3. Research Question

> **How does Neobractatin treatment alter gene expression and biological pathways in HeLa cells?**

The project investigates transcriptional changes associated with processes such as:

- DNA damage response
- Apoptosis
- Cell-cycle regulation
- Cellular stress responses
- Metabolic processes
- Cancer-related signalling

---

## 4. Biological Context

**HeLa cells** are a human cancer cell line used as a model for studying cancer biology and cellular responses to treatments.

The project focuses on **Neobractatin**, a natural compound reported to have anti-cancer effects.

By comparing Neobractatin-treated cells with DMSO controls at the RNA level, we can investigate which genes and biological pathways are affected by the treatment.

---

## 5. Dataset

The project uses publicly available RNA-seq data from the **NCBI Gene Expression Omnibus (GEO)**.

| Property | Information |
|---|---|
| GEO accession | **GSE108706** |
| Organism | *Homo sapiens* |
| Cell line | HeLa |
| Data type | Bulk RNA-seq |
| Conditions | DMSO control vs Neobractatin treatment |
| Biological replicates | 3 per condition |
| Total samples | 6 |
| Sequencing platform | Illumina HiSeq X Ten |
| Read type | 150 bp paired-end |
| Raw data | FASTQ |
| Reference genome | Human hg38 |

The dataset therefore has:

```text
HeLa cells
     │
     ├───────────────┐
     ↓               ↓
DMSO Control     Neobractatin
   n = 3             n = 3
     │               │
     └───────┬───────┘
             ↓
          RNA-seq
             ↓
       Transcriptome
        analysis
```

---

## 6. Main Objectives

The project objectives were to:

1. Obtain publicly available RNA-seq data for Neobractatin-treated and control HeLa cells.
2. Assess the quality of raw sequencing reads.
3. Remove adapter contamination and low-quality bases.
4. Align cleaned reads to the human reference genome.
5. Generate gene-level expression counts.
6. Identify differentially expressed genes between treatment and control groups.
7. Visualize transcriptomic differences using PCA, heatmaps, and volcano plots.
8. Perform Gene Ontology (GO) and KEGG pathway enrichment analysis.
9. Interpret the transcriptional changes in a biological context.

---

## 7. Overall Workflow

```text
Raw FASTQ files
       ↓
Quality Control
       ↓
FastQC
       ↓
MultiQC
       ↓
Read Trimming
       ↓
Adapter / Low-quality base removal
       ↓
Cleaned reads
       ↓
Genome Alignment
       ↓
HISAT2
       ↓
Human reference genome (hg38)
       ↓
Gene-level Quantification
       ↓
featureCounts / HTSeq
       ↓
Gene Count Matrix
       ↓
Differential Expression
       ↓
DESeq2
       ↓
PCA / Heatmap / Volcano Plot
       ↓
Functional Enrichment
       ↓
GO / KEGG
       ↓
Biological Interpretation
```

---

## 8. Tools Used

| Stage | Tool / Software | Purpose |
|---|---|---|
| Quality control | FastQC | Assess raw read quality |
| QC summary | MultiQC | Combine QC results |
| Trimming | Read-trimming software | Remove adapters and low-quality bases |
| Alignment | HISAT2 | Align reads to hg38 |
| Quantification | featureCounts / HTSeq | Generate gene-level counts |
| Statistical analysis | DESeq2 | Differential expression |
| Visualization | R / plotting tools | PCA, heatmaps, volcano plots |
| Functional analysis | GO / KEGG | Biological interpretation |

---

## 9. Main Comparison

The central comparison in the project is:

```text
Neobractatin-treated HeLa cells
                VS
DMSO-treated HeLa cells
```

The purpose is to determine:

```text
What genes change?
        ↓
How strongly do they change?
        ↓
Which genes are significantly different?
        ↓
What biological pathways are affected?
        ↓
What might these changes tell us about
the response to Neobractatin?
```

---

## 10. Major Analysis Questions

At each stage, the project asks a different question.

| Stage | Question |
|---|---|
| Quality control | Are the sequencing reads of sufficient quality? |
| Trimming | Can unwanted adapters/low-quality regions be removed? |
| Alignment | Where do the reads map in the human genome? |
| Quantification | How many reads are associated with each gene? |
| Count matrix | What is the expression/count profile across samples? |
| PCA / clustering | How are the samples related to each other? |
| Differential expression | Which genes differ between conditions? |
| Functional enrichment | What biological processes/pathways are associated with these genes? |
| Interpretation | What might the results mean biologically? |

---

## 11. Expected Analysis Output

The project ultimately produces several types of results.

### Quality Results

- Per-base sequencing quality
- GC content
- Read length
- Duplication
- Adapter contamination
- Alignment efficiency

### Expression Results

- Gene-level count matrix
- Normalized expression data
- Sample relationships

### Differential Expression Results

- Log2 fold changes
- p-values
- Adjusted p-values / FDR
- Upregulated genes
- Downregulated genes

### Visualization

- PCA plots
- Heatmaps
- Volcano plots

### Functional Results

- Gene Ontology enrichment
- KEGG pathway enrichment

---

## 12. Reported Project Findings

The internship report describes the following major findings:

- The six samples showed generally high sequencing quality.
- Most bases had Phred quality scores above 30.
- GC content was approximately 49–50%.
- HISAT2 alignment to hg38 achieved approximately 92–95% overall alignment.
- PCA showed separation between DMSO control and Neobractatin-treated samples.
- Biological replicates clustered consistently within their respective groups.
- DESeq2 identified **1,247 differentially expressed genes**.
- **682 genes were upregulated**.
- **565 genes were downregulated**.
- Upregulated genes were associated with processes including DNA damage response, p53 signalling, and apoptosis.
- Downregulated genes were associated with metabolic and cell-cycle-related processes.

---

## 13. Biological Interpretation

The reported results indicate that Neobractatin treatment produces a clear transcriptomic response in HeLa cells.

The increased representation of pathways related to:

- DNA damage
- p53 signalling
- Cellular stress
- Apoptosis

is consistent with a response involving growth inhibition and programmed cell death.

Changes in:

- Metabolic processes
- Cell-cycle-related genes

suggest effects on processes involved in cellular growth and proliferation.

The RNA-seq analysis therefore connects changes in gene expression with possible molecular mechanisms underlying the response to Neobractatin.

---

## 14. Project Structure

The project can be understood as four broad stages:

```text
                PROJECT
                   │
       ┌───────────┴───────────┐
       ↓                       ↓
   RNA-seq                 Interpretation
   Analysis                    │
       │                       │
       ├── QC                  ├── DEGs
       ├── Trimming            ├── GO
       ├── Alignment           ├── KEGG
       ├── Counting            └── Biological meaning
       └── DE analysis
```

For this reconstructed learning project, the emphasis is on understanding **why each step is performed**, not simply rerunning old commands.

---

## 15. Learning Goal

The goal of reconstructing this project is to understand a complete **bulk RNA-seq analysis workflow** from raw sequencing data to biological interpretation.

I should eventually be able to explain:

```text
What is the biological question?
        ↓
What data were used?
        ↓
What are FASTQ files?
        ↓
How do we assess read quality?
        ↓
Why do we trim reads?
        ↓
How are reads aligned?
        ↓
How are genes quantified?
        ↓
What is a count matrix?
        ↓
Why do we normalize?
        ↓
How do we compare samples?
        ↓
How do we identify DEGs?
        ↓
What do DEGs mean biologically?
        ↓
How do GO and KEGG help?
        ↓
How do we interpret the final results?
```

---

## 16. Project Goal

> **To reconstruct and understand the complete bulk RNA-seq workflow used to investigate the transcriptional response of HeLa cells to Neobractatin treatment, from raw sequencing reads through differential expression and functional interpretation.**

---

## 17. Important Note

This repository is being used not only to reproduce the internship project but also to **relearn the concepts behind each step**.

The learning approach is:

```text
Learn the concept
       ↓
Understand why it is needed
       ↓
Run the analysis
       ↓
Interpret the output
       ↓
Document the result
       ↓
Move to the next step
```

The detailed concepts, commands, tools, and troubleshooting will be documented in the remaining notes sections.

---

## 18. Key Takeaways

- This is a **bulk RNA-seq** project.
- The biological system is **HeLa cells**.
- The treatment is **Neobractatin (NBT)**.
- **DMSO** is the control condition.
- The dataset is **GSE108706**.
- There are **3 biological replicates per condition**, giving 6 samples.
- The sequencing data are **150 bp paired-end Illumina reads**.
- The reference genome used was **human hg38**.
- **HISAT2** was used for alignment.
- **featureCounts / HTSeq** were used for gene-level quantification.
- **DESeq2** was used for differential expression analysis.
- **GO and KEGG** were used for functional interpretation.
- The reported analysis identified **1,247 DEGs**.
- The overall purpose is to understand how Neobractatin changes the transcriptome of HeLa cells.

---

## 19. Primary Source

**Internship Report:**  
*RNA-Sequencing Based Transcriptome Analysis of Neobractatin-Treated HeLa Cells*

**Dataset:**  
GEO accession **GSE108706**

**Project type:**  
Bulk RNA-seq transcriptome analysis
