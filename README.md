# RNA_Sequencing_Based_Transcriptome_Analysis_of_Neobractatin_Treated_HeLa_Cells
This repository documents my one-month MSc Bioinformatics internship project focused on RNA-Seq transcriptome analysis of Neobractatin-treated HeLa cells. It includes the complete computational workflow, project notes, scripts, results, presentation slides and report developed during the internship.

## Overview

This repository documents my one-month MSc Bioinformatics internship project focused on investigating the transcriptomic response of HeLa cells to the natural compound **Neobractatin** using publicly available bulk RNA-Seq data.

The study compares **Neobractatin-treated HeLa cells** with **DMSO-treated control cells** to identify differentially expressed genes and biological pathways associated with the cellular response to Neobractatin.

The project covers a complete RNA-Seq analysis workflow, from raw sequencing data quality assessment to differential expression and functional enrichment analysis.

---

## Research Question

**How does Neobractatin treatment alter gene expression and biological pathways in HeLa cells?**

The analysis aims to identify transcriptional changes associated with processes such as:

- DNA damage response
- Apoptosis
- Cell-cycle regulation
- Cellular stress responses
- Metabolic processes
- Cancer-related signalling pathways

---

## Dataset

The analysis uses the publicly available RNA-Seq dataset:

**GEO Accession:** `GSE108706`

### Experimental design

| Group | Treatment | Biological Replicates |
|---|---|---:|
| Control | DMSO | 3 |
| Treatment | Neobractatin (NBT) | 3 |

### Sequencing information

- Organism: *Homo sapiens*
- Cell line: HeLa
- Sequencing platform: Illumina HiSeq X Ten
- Read type: 150 bp paired-end
- Data type: Bulk RNA-Seq
- Reference genome: Human hg38

---

## Analysis Workflow

The overall computational workflow was:

```text
Raw FASTQ files
       │
       ▼
Quality Control
(FastQC)
       │
       ▼
Quality Summary
(MultiQC)
       │
       ▼
Adapter & Quality Trimming
       │
       ▼
Cleaned Reads
       │
       ▼
Genome Alignment
(HISAT2 → hg38)
       │
       ▼
Gene-Level Quantification
(featureCounts / HTSeq)
       │
       ▼
Count Matrix
       │
       ▼
Differential Expression
(DESeq2)
       │
       ├───────────────┐
       ▼               ▼
    PCA              DEGs
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
        Volcano Plot          Heatmap
             │
             ▼
    Functional Enrichment
             │
       ┌─────┴─────┐
       ▼           ▼
      GO          KEGG
       │           │
       └─────┬─────┘
             ▼
      Biological Interpretation
