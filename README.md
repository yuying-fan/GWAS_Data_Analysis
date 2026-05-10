# GWAS Pipeline for Antifungal Drug Resistance in *Aspergillus fumigatus*
_Author: Yuying Fan_  
_Pipeline developed during MSc at McMaster University in Dr. Jianping Xu's lab, 2019-2021_  

## Project Aim - Reproducible Genome-Wide Association Pipeline for Fungal Drug Resistance Discovery
This project began as a graduate-course assignment for BIO722 (*Introduction to Bioinformatic Methods*) at McMaster University, where the pipeline was developed and run on a high-performance computing cluster using a curated subset of samples. The protocol was subsequently extended and applied at full scale to my MSc thesis work in Dr. Jianping Xu's lab ([University Profile](https://experts.mcmaster.ca/display/jpxu), [Lab Website](https://xulabmcmaster.wordpress.com/pi-biography/)), and became the foundation for three peer-reviewed publications ([1](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7713013/), [2](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8227032/), [3](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8538161/)) and a conference poster presented at the 31st Fungal Genetics Conference (see *Publications & Presentations* below).

This repository documents an end-to-end GWAS workflow from raw whole-genome sequencing reads to functionally annotated, phenotype-associated SNPs - applied to identifying genetic determinants of antifungal drug resistance in the opportunistic fungal pathogen, *Aspergillus fumigatus*.

## Background

*Aspergillus fumigatus* is a ubiquitous saprophytic mold and the leading cause of invasive aspergillosis, a life-threatening infection in the immunocompromised population. Triazoles (particularly itraconazole and voriconazole) are first-line antifungals used against aspergillosis, but rising triazole resistance worldwide has increased the importance of second-line agents like amphotericin B (AMB). Amphotericin B is a polyene that has been widely used for over 60 years as salvage therapy for refractory aspergillosis. AMB is also recommended as primary therapy in regions with ≥10% environmental triazole resistance and patients with invasive aspergillosis caused by triazole-resistant strains carry a mortality rate of ~88%, making AMB efficacy critical. 

AMB resistance has historically been uncommon for a fungicidal agent. However, recent surveillance has reported strikingly high resistance rates (MIC ≥ 2 mg/L) in specific geographic populations for reasons that remain unclear; 96.4% in Hamilton, Canada and 27% in Campinas, Brazil. AMB's molecular mechanisms in *A. fumigatus* are also poorly characterized: multiple models have been proposed (ion-channel formation, ROS induction, surface absorption, sterol-sponge extraction of ergosterol) and the genetic determinants of resistance remain largely unexplored beyond a handful of candidate genes. 

Genome-wide association studies (GWAS) test for statistical association between common single-nucleotide polymorphisms (SNPs) and quantitative phenotypes such as minimum inhibitory concentrations (MICs). Applied across a wide range of clinical and environmental *A. fumigatus* isolates, GWAS can help determine novel resistance-associated loci beyond the canonical mechanisms - informing diagnostic marker development, surveillance strategies, and downstream functional studies.

## Objective
To document a reproducible, cluster-deployable GWAS pipeline covering:
- Preparing whole-genome sequencing reads and reference-genome
- Read-level quality control, adapter trimming, and reference alignment
- Variant calling, sample- and variant-level QC, and phenotype normalization to produce association-ready inputs
- Genome-wide association testing on the normalized quantitative phenotype, using PLINK (linear regression) and TASSEL (GLM), using top principal components as covariates to control for population stratification
- Visualization of association results (Manhattan and Q–Q plots)
- Functional annotation of top SNPs and candidate-gene interpretation

>### Scope
>
> This protocol was developed for haploid fungal genomes (*A. fumigatus*). It uses a subset of *A. fumigatus* isolates for coursework demonstration; but these methods were used as the foundation for full-cohort analyses underlying my MSc thesis and the linked publications.
> Core tools: `FastQC`, `Trimmomatic`, `BWA`, `samtools`, `GATK`, `vcftools`, `PLINK`, `TASSEL`, and `R` for visualization and downstream annotation.

## Folder Structure

```
GWAS_Data_Analysis/
├── README.md
├── 1.Whole_Genome_Sequences.md
├── 2.Quality_Control_and_Trimming.md
├── 3.Alignment_and_Variant_Calling.md
├── 4.Quality_Control_and_Prep_for_Association_Analysis.md
├── 5.GWAS_with_Plink_and_Tassel.md
├── 6.Visualization_of_GWAS_Results.md
├── 7.SNP_Annotation.md
└── Images/                            ← Manhattan plots, QQ plots, and supporting visuals
```

## File Contents
- `1.Whole_Genome_Sequences.md` - Sample retrieval from NCBI, *A. fumigatus* reference genome download and BWA indexing
- `2.Quality_Control_and_Trimming.md` - Pre-alignment QC, adapter and quality trimming, post-trim re-QC  
- `3.Alignment_and_Variant_Calling.md` - Alignment to the reference genome, sorting, deduplication, haploid variant calling  
- `4.Quality_Control_and_Prep_for_Association_Analysis.md` - Variant filtering, LD pruning, clonal-strain removal, phenotype-file preparation
- `5.GWAS_with_Plink_and_Tassel.md` - Association testing in PLINK (linear regression) and TASSEL (GLM)
- `6.Visualization_of_GWAS_Results.md` — Manhattan plots, QQ plots
- `7.SNP_Annotation.md` - Top 10 SNP extraction by p-value (for PLINK and TASSEL), variant annotation, gene-function lookup 

## Publications & Presentations

**Peer-reviewed publications building on this pipeline:**
- [Paper 1 — PMC7713013](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7713013/)
- [Paper 2 — PMC8227032](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8227032/)
- [Paper 3 — PMC8538161](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8538161/)

**Conference presentation:**  
- *"Genomic and Genetic Analyses of Antifungal Drug Resistance in Aspergillus fumigatus"* - 31st Fungal Genetics Conference, 2022 ([program book](https://genetics-gsa.org/fungal-2022/wp-content/uploads/sites/36/2022/03/220316-Fungal22-Program-Book-v3.pdf)). Poster presented by Dr. Jianping Xu; contents drafted by Yuying Fan based on MSc thesis work.
