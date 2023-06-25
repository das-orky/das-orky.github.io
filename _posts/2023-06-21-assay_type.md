---
layout: single
classes: wide
author_profile: false
sidebar:
  nav: "foo_all"
header:
  overlay_image: /assets/images/post_dna_assay.jpg
  caption: "(CC) UIUC"
title: "Different types of DNA assays"
excerpt: >
  A list of various kinds of DNA assays out there in the wild<br />
categories:
  - Genomics
tags:
  - dna assay
  - sequencing technique
---

The assay zoo, there is no ordering, this list is not exhaustive:

* ChIP-seq
* Hi-C
* DNase-seq
* SMRT
* ATAC-seq
* FAIRE-seq
* ChIP-exo
* RNA-seq
* scRNA-seq
* Drop-seq
* scATAC-seq
* MeDIP-seq
* CUT&RUN
* Metagenomics
* Nanopore sequencing
* Whole genome sequencing

**<u>ChIP-seq (Chromatin Immunoprecipitation sequencing)</u>**: It is a method employed for the identification of DNA binding sites of transcription factors and other proteins, serving as a robust tool for investigating gene regulation and epigenetics. Moreover, it has been extensively utilized in the examination of gene expression regulation and the comprehensive mapping of genome-wide distributions of histone modifications. However, it is important to note that this technique can be time-consuming and may present challenges in discerning between active and inactive binding sites.
{: .text-justify}

**<u>Hi-C (Chromatin Conformation Capture)</u>**: Hi-C is a powerful genomics technique that provides insights into the three-dimensional organization of chromatin in the nucleus. It reveals the spatial proximity and interactions between different genomic regions, offering a comprehensive view of genome architecture and its influence on gene regulation and genome function. Hi-C maps topologically associating domains (TADs), which are self-interacting genomic regions. TADs are thought to play a crucial role in gene regulation, as genes within the same TAD tend to interact with each other more frequently than with genes in neighboring TADs. Hi-C data also provides insights into the higher-order chromatin structures, such as chromatin loops, compartments, and the spatial positioning of chromosomes. 
{: .text-justify}

**<u>DNase-seq (DNase I hypersensitive sites sequencing)</u>**: It is a technique used to identify regions of the genome that are accessible to DNase I, an enzyme that cleaves DNA. Useful in studying gene regulation and epigenetics, it makes significant advances in our understanding of how genes are turned on and off. This technique identifies regions of the genome that are accessible to transcription factors and also maps the genome-wide distribution of open chromatin. It has higher sensitivity towards promoter regions.
How is it differ from ChIP-seq?. ChIP-seq measures the binding sites of transcription factors, while DNase-seq measures the accessibility of DNA to DNase I, an enzyme that cleaves DNA.
{: .text-justify}

**<u>SMRT (Single-molecule real-time)</u>**: It offers long-read sequencing capabilities with high accuracy. It enables the direct observation and sequencing of individual DNA molecules in real-time, providing valuable insights into genome structure, DNA modifications, and complex genomic variations. It produces long sequencing reads, often spanning several kilobases or even tens of kilobases in length. It can detect various DNA modifications, including DNA methylation and other base modifications.  
{: .text-justify}

**<u> ATAC-seq (Assay for transposase-accessible chromatin with sequencing)</u>**: It is also a powerful and widely used technique in the field of genomics and epigenetics. It allows researchers to investigate the accessibility of chromatin regions in a genome-wide manner.It can identify genomes that are accessible to transcription factors. It can also study gene regulation and identification of open chromatin. The difference between ChIP-seq and DNase-seq is that it can sequence open chromatin regions with a resolution of a single nucleotide. 
{: .text-justify}

**<u>FAIRE-seq (Formaldehyde-Assisted Isolation of Regulatory Elements)</u>**: This technique is employed to investigate the accessibility of chromatin, which refers to the organization and compaction of DNA within the cellular nucleus. Notably, it offers the advantage of directly analyzing various cell types without the requirement for additional nucleus separation or complex procedures. It demonstrates enhanced coverage specifically in the enhancer region, enabling detailed examination of regulatory elements. However, it is important to consider that the signal-to-noise ratio of chromatin accessibility can be comparatively lower due to the presence of an augmented background level.
{: .text-justify}

**<u>ChIP-exo (Chromatin immunoprecipitation with exonuclease digestion)</u>**: It is a technique used to identify the binding sites of DNA-associated proteins with single-nucleotide resolution. It is a modification of the ChIP-seq protocol that improves the resolution of binding sites from hundreds of base pairs to almost one base pair. It is less prone to contamination of non-protein-bound DNA fragments, which can lead to low false positives and negatives. It can be used to study proteins that bind weakly to DNA. It requires less depth of sequencing since it has higher resolution and low background noise. One of its disadvantages is that for a single binding event, if there are multiple protein-DNA complexes, then instead of a single binding event it will be thought of as multiple binding events.
{: .text-justify}

**<u>RNA-seq (RNA sequencing)</u>**: Is a powerful and widely used technique that allows researchers to investigate the transcriptome, it provides a snapshot of the RNA molecules present in a sample. It is a quantitative approach (which means that it can be used to measure the abundance of transcripts.) to study gene expression, alternative splicing, identification of novel transcripts, and characterization of non-coding RNAs. It can be used to identify genes that are differentially expressed in different cell types or under different conditions.
{: .text-justify}

**<u>scRNA-seq (Single cell RNA sequencing)</u>**: Single-cell RNA sequencing (scRNA-seq) represents a cutting-edge technique that revolutionizes the analysis of gene expression profiles at the individual cell level. It serves as a powerful tool for unraveling cellular heterogeneity, identifying rare cell populations, and elucidating the dynamic processes within cells. By capturing the transcriptomes of thousands to millions of individual cells within a sample, scRNA-seq provides unprecedented resolution, enabling comprehensive insights into the molecular characteristics of each cell. This technique unveils dynamic gene expression patterns during various biological processes such as development, disease progression, and response to treatments. Moreover, scRNA-seq facilitates the characterization of cell-to-cell interactions in response to diverse stimuli and the identification of intricate gene regulatory networks, further enhancing our understanding of cellular behavior.
{: .text-justify}

**<u>Drop-seq (Single-Cell RNA-seq with Droplet Technology)</u>**: It is a single-cell RNA sequencing (scRNA-seq) technique with droplet technology that enables the analysis of gene expression in individual cells on a large scale. It presents a high-throughput and cost-effective approach for studying the transcriptomes of thousands of cells concurrently, offering valuable insights into cellular heterogeneity, gene regulation, and cell type identification. This technique excels in throughput compared to traditional scRNA-seq methods, facilitating the profiling of tens of thousands of cells within a single experiment. Notably, it exhibits remarkable sensitivity, enabling the capture of low-abundance transcripts and enabling the detection of rare cell types or genes that might otherwise go unnoticed.
{: .text-justify}

**<u>scATAC-seq (Single cell ATAC-seq)</u>**: Is a state-of-the-art technique that allows researchers to investigate the chromatin accessibility of individual cells. It provides a comprehensive view of the regulatory landscape within a heterogeneous cell population, enabling the characterization of cell types, identification of regulatory elements, and exploration of epigenetic dynamics at single-cell resolution. It can analyze the accessibility of specific genomic regions, researchers can identify and annotate cell type-specific regulatory elements and assess their potential impact on gene expression. If integrated with scRNA-seq the relationships between chromatin accessibility and gene expression patterns can be found. 
{: .text-justify}

**<u>MeDIP-seq (Methylated DNA Immunoprecipitation sequencing)</u>**: It is a technique used to investigate DNA methylation patterns across the genome and their functional significance. It provides a high-throughput and genome-wide approach to analyze DNA methylation, which is an essential epigenetic modification involved in gene regulation. Such analysis can reveal epigenetic changes associated with aging, and disease (e,g cancer). 
{: .text-justify}

**<u>CUT&RUN (Cleavage Under Targets & Release Using Nuclease)</u>**: It is a method for profiling protein-DNA interactions with high resolution and low background noise. It offers a streamlined and efficient approach to investigate transcription factor binding, chromatin modifications, and other protein-DNA interactions in the genome. It has a higher signal-to-noise ratio and specificity in identifying binding sites compared to ChIP-seq. It also requires fewer cells to perform the sequencing.
{: .text-justify}

**<u>Metagenomics</u>**: Is a field of biology that studies the genetic material of entire communities of microorganisms. It is a powerful tool for studying the microbial diversity of an environment, and for identifying new microorganisms and genes. Metagenomics has been used to study a wide range of environmental samples, including soil, water, air, and even the human gut. It has been used to identify new microorganisms, to study the evolution of microbial communities, and to understand the role of microorganisms in the environment. 
{: .text-justify}

**<u>Nanopore sequencing</u>**: It offers real-time, long-read sequencing as the DNA or RNA molecules pass through nanopores.It has the ability to generate long sequencing reads, often ranging from thousands to tens of thousands of bases in length. Long reads help in facilitating the assembly of genomes, especially in areas with repetitive sequences. It can also detect DNA modifications, like DNA methylation. 
{: .text-justify}


**<u>Whole genome sequencing (WGS)</u>**: It is an approach to sequencing an individual's entire genome. It involves the determination of the complete DNA sequence of an organism's genome, providing a detailed blueprint of the genetic information encoded within an individual's DNA. It allows the identification of single nucleotide variations (SNVs), insertions and deletions (indels), copy number variations (CNVs), structural variations (SVs), and other genomic alterations. This information may help in finding the role of genes in disease.   
{: .text-justify}

