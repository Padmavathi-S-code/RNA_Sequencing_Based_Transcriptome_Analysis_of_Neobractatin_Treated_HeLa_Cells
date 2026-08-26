# RNA-Sequencing Based Transcriptome Analysis of Neobractatin-Treated HeLa Cells

This repository documents my one-month MSc Bioinformatics internship project focused on RNA-Seq transcriptome analysis of Neobractatin-treated HeLa cells.

It contains the internship thesis and presentation, along with a summary of the research question, experimental design, computational workflow, key findings, and biological interpretation.

---

## Overview

This project investigates the transcriptomic response of **HeLa cells to Neobractatin (NBT)** using publicly available bulk RNA-Seq data.

The study compares **Neobractatin-treated HeLa cells** with **DMSO-treated control cells** to identify differentially expressed genes and biological pathways associated with the cellular response to Neobractatin.

The project follows a bulk RNA-Seq analysis workflow starting from raw sequencing reads and quality control, followed by read processing, genome alignment, gene-level quantification, differential expression analysis, and functional enrichment.

---

## Research Question

**How does Neobractatin treatment alter gene expression and biological pathways in HeLa cells?**

The analysis was designed to identify transcriptional changes associated with:

- DNA damage response
- Apoptosis
- Cell-cycle regulation
- Cellular stress responses
- Metabolic processes
- Cancer-related signalling pathways

---

## Objectives

The main objectives of the project were to:

1. Obtain and analyse publicly available RNA-Seq data for Neobractatin-treated and control HeLa cells.
2. Assess the quality of the raw sequencing reads.
3. Remove adapter contamination and low-quality bases.
4. Align cleaned reads to the human reference genome.
5. Generate gene-level expression counts.
6. Identify differentially expressed genes between treated and control groups.
7. Visualize transcriptomic differences using PCA, heatmaps, and volcano plots.
8. Perform Gene Ontology (GO) and KEGG pathway enrichment analysis.
9. Interpret the identified transcriptional changes in a biological context.

---

## Dataset

The analysis used publicly available bulk RNA-Seq data from the **NCBI Gene Expression Omnibus (GEO)**.

### Dataset Information

| Property | Information |
|---|---|
| GEO accession | **GSE108706** |
| Organism | *Homo sapiens* |
| Cell line | HeLa |
| Experimental conditions | DMSO control vs Neobractatin (NBT) |
| Biological replicates | 3 per condition |
| Total samples | 6 |
| Sequencing platform | Illumina HiSeq X Ten |
| Read type | 150 bp paired-end |
| Data format | FASTQ |
| Reference genome | Human hg38 |
| Data type | Bulk RNA-Seq |

The dataset contains three DMSO control samples and three Neobractatin-treated samples.

---

## Experimental Design

```text
                    HeLa Cells
                        │
             ┌──────────┴──────────┐
             │                     │
       DMSO Control          Neobractatin
        n = 3                    n = 3
             │                     │
             └──────────┬──────────┘
                        │
                     RNA-Seq
                        │
                  FASTQ files
                        │
                        ▼
              Transcriptome Analysis
```

### Main Comparison

**Neobractatin-treated HeLa cells**

vs.

**DMSO-treated HeLa cells**

---

## Analysis Workflow

The overall computational workflow was:

```text
Raw FASTQ files
       │
       ▼
Quality Control
FastQC
       │
       ▼
QC Summary
MultiQC
       │
       ▼
Adapter & Low-quality Base Trimming
       │
       ▼
Cleaned Reads
       │
       ▼
Genome Alignment
HISAT2
       │
       ▼
Human Reference Genome
hg38
       │
       ▼
Gene-level Quantification
featureCounts / HTSeq
       │
       ▼
Gene Count Matrix
       │
       ▼
Differential Expression Analysis
DESeq2
       │
       ├──────────────┬───────────────┐
       ▼              ▼               ▼
      PCA        Volcano Plot      Heatmap
       │
       └──────────────┬────────────────┘
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
```

The workflow follows the progression from raw FASTQ data through quality control, read processing, alignment, gene-level quantification, differential expression, and functional analysis.

---

## Tools & Technologies

### Quality Control

#### FastQC

Used to assess the quality of raw sequencing reads, including:

- Per-base sequence quality
- GC content
- Sequence length
- Duplication levels
- Adapter contamination

#### MultiQC

Used to combine and summarize FastQC results across all six samples.

---

### Read Processing

- Adapter removal
- Low-quality base trimming
- Paired-end read filtering

---

### Genome Alignment

#### HISAT2

Used to align cleaned RNA-Seq reads to the human reference genome.

- Reference genome: **hg38**
- Splice-aware alignment
- Output: SAM/BAM alignment files

---

### Gene-Level Quantification

#### featureCounts / HTSeq

Used for assigning aligned reads to annotated genes and generating a gene-level count matrix.

The resulting count matrix contains:

| Component | Description |
|---|---|
| Rows | Genes |
| Columns | Samples |
| Values | Read counts |

---

### Differential Expression Analysis

#### R

Used as the statistical analysis environment.

#### DESeq2

Used to identify genes whose expression differed between:

- DMSO control
- Neobractatin treatment

DESeq2 was used for count normalization, dispersion estimation, and statistical testing for differential expression.

---

### Statistical Analysis & Visualization

The project used:

- Principal Component Analysis (PCA)
- Hierarchical clustering
- Heatmaps
- Volcano plots
- Log2 fold-change analysis
- Adjusted p-values / FDR
- Differential expression statistics

---

### Functional Analysis

The differentially expressed genes were further analysed using:

- Gene Ontology (GO) enrichment
- KEGG pathway enrichment

These analyses were used to connect gene-level changes with biological processes and signalling pathways.

---

# Results

## 1. Raw Read Quality

FastQC analysis of all six samples showed generally high sequencing quality.

The analysis observed:

- Most bases had Phred quality scores above 30.
- GC content was approximately 49–50%.
- Reads were consistently 150 bp paired-end.
- Duplication levels were considered acceptable for the deeply sequenced RNA-Seq libraries.
- No major sequencing-quality problems were identified.

MultiQC was used to summarize the QC results across all samples.

---

## 2. Read Alignment

After trimming, cleaned reads were aligned to the human **hg38** reference genome using HISAT2.

The reported overall alignment rates were:

**92–95% across the samples**

More specifically:

| Metric | Result |
|---|---|
| DMSO alignment | 93.2 ± 1.1% |
| Neobractatin alignment | 94.1 ± 0.8% |
| Concordantly aligned pairs | 85–88% |
| Multi-mappers | <2% |

These results indicate that the sequencing reads aligned efficiently to the reference genome.

---

## 3. Exploratory Data Analysis

Principal Component Analysis (PCA) was performed using normalized gene-level count data.

The PCA showed clear separation between:

- DMSO control samples
- Neobractatin-treated samples

Biological replicates within each condition clustered closely together.

Hierarchical clustering and heatmap analysis of highly variable genes showed a similar separation between the two experimental groups.

This suggests that the treatment condition was a major source of variation in the dataset.

---

## 4. Differential Gene Expression

Differential expression analysis was performed using **DESeq2**.

The main significance criteria were:

```text
FDR < 0.05
|log2 fold change| > 1
```

### Differential Expression Summary

| Category | Number of genes |
|---|---:|
| Total DEGs | **1,247** |
| Upregulated | **682** |
| Downregulated | **565** |

### Examples of Upregulated Genes

- **CDKN1A**
- **MDM2**
- **BBC3**

### Examples of Downregulated Genes

- **HMGCS1**
- **FASN**
- **E2F1**

The analysis associated many upregulated genes with stress response and chromatin organization, while several downregulated genes were associated with metabolic and cell-cycle related functions.

---

## 5. Functional Enrichment

GO and KEGG enrichment analyses were performed to investigate the biological meaning of the differentially expressed genes.

### Upregulated Pathways and Processes

The analysis highlighted pathways and processes associated with:

- DNA damage response
- p53 signalling
- MAPK/NF-κB signalling
- Apoptotic processes
- Cellular stress responses

### Downregulated Pathways and Processes

Downregulated genes were associated with:

- Fatty acid metabolism
- Sulfur metabolism
- Other biosynthetic pathways
- Metabolic processes associated with cellular growth
- Cell-cycle related functions

These findings were consistent with the biological interpretation presented in the internship report.

---

## Biological Interpretation

The analysis indicates that Neobractatin treatment produces a clear and reproducible transcriptomic response in HeLa cells.

The increased representation of pathways related to **DNA damage response, p53 signalling, cellular stress, and apoptosis** is consistent with a cellular response involving growth inhibition and programmed cell death.

At the same time, changes in metabolic and cell-cycle related genes suggest effects on processes that support cellular growth and proliferation.

Overall, the RNA-Seq analysis connects transcriptional changes observed after Neobractatin treatment with potential molecular mechanisms underlying its reported biological effects.

This interpretation is based on the differential expression and functional enrichment results described in the internship report.

---

## Key Findings

The main findings of the project can be summarized as:

- High-quality sequencing data were obtained across all six samples.
- Most bases showed Phred quality scores above 30.
- GC content was approximately 49–50%.
- HISAT2 alignment to hg38 achieved approximately **92–95% overall alignment**.
- PCA showed clear separation between control and treated samples.
- Biological replicates clustered consistently within their respective groups.
- DESeq2 identified **1,247 differentially expressed genes**.
- **682 genes were upregulated**.
- **565 genes were downregulated**.
- Upregulated genes were associated with DNA damage, p53 signalling, and apoptosis-related processes.
- Downregulated genes were associated with metabolic and cell-cycle related processes.

---

## Repository Structure

```text
RNA_Sequencing_Based_Transcriptome_Analysis_of_Neobractatin_Treated_HeLa_Cells/
│
├── presentation/
│   └── 24L10925_RNASeq_Internship_Presentation_M.Sc_Bioinformatics.pptx
│
├── thesis/
│   └── Internship_Report_RNA-Seq_Bioinformatics-1.pdf
│
├── README.md
│
└── LICENSE
```

---

## Learning Outcomes

This internship provided practical experience in:

- Bulk RNA-Seq analysis
- FASTQ sequencing data
- Sequencing quality control
- FastQC and MultiQC
- Read trimming
- Reference genome alignment
- HISAT2
- SAM/BAM files
- Gene-level quantification
- Count matrices
- Differential expression analysis
- R and DESeq2
- PCA and clustering
- Heatmap and volcano plot visualization
- GO enrichment
- KEGG pathway analysis
- Biological interpretation of transcriptomic results
- Linux-based bioinformatics workflows

An important learning outcome was understanding how individual bioinformatics tools fit together into a complete analysis pipeline and how computational results can be connected back to a biological research question.

---

## Limitations

This project used **bulk RNA-Seq**, which provides an overall transcriptomic profile across the sampled cell population.

Because bulk RNA-Seq averages expression across cells, it cannot directly resolve differences between individual cellular subpopulations.

---

## Future Work

Potential extensions of this project include:

- Reproducing the complete analysis pipeline with documented scripts
- Adding analysis notebooks and scripts to the repository
- Adding processed count matrices and result tables where appropriate
- More detailed pathway and network analysis
- Investigation of upstream regulatory mechanisms
- Validation of selected candidate genes
- Integration with additional omics datasets
- Single-cell RNA-Seq analysis
- Comparison with additional cancer-cell models

---

## Internship Documentation

### Thesis

The complete MSc Bioinformatics internship thesis is available in:

`thesis/Internship_Report_RNA-Seq_Bioinformatics-1.pdf`

### Presentation

The internship presentation is available in:

`presentation/24L10925_RNASeq_Internship_Presentation_M.Sc_Bioinformatics.pptx`

---

## References

The detailed references used for this project are provided in the internship thesis.

---

## Author

**Padmavathi S**

MSc Bioinformatics  
JSS Academy of Higher Education & Research, Mysuru

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.