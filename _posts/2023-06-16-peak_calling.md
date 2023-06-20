---
layout: single
classes: wide
author_profile: false
sidebar:
  nav: "foo_all"
header:
  overlay_image: /assets/images/post_peak_calling.jpg
  caption: "(Creative Commons)"
title: "Peak Calling"
excerpt: >
  To find regions in DNA that are enriched. Which helps in gain valuable insights into gene regulation, epigenetic modifications, and other fundamental biological processes.<br />
categories:
  - Genomics
tags:
  - peak calling
  - dna accessibility
---

# Peak calling:

How do you and I differ?. How do the cells of different body organs or tissue differ in an individual?. The variance can be attributed to the diverse expression of cellular characteristics, like, the range of proteins produced, the intricate interactions between cells. Such outcomes, influenced by protein synthesis and signaling mechanisms, and many other features contribute to the differentiation of cell types within an organism, as well as between individuals of the same organism (e.g., Homo sapiens). It is worth noting that our developmental process commences with a single sperm cell fusing with a female egg, initiating the process of morphogenesis.
{: .text-justify}

The DNA within our cells undergoes a process of coiling, resulting in a compacted structure where only the essential regions are exposed of that cell type. The accessibility of these regions can vary depending on the stage of life cycle the cell is undergoing. Let's look at how DNA is coiled in a cell:
{: .text-justify}

![image-center](/assets/images/peak_call_1.jpg){: .align-center}
https://en.wikipedia.org/wiki/Epigenetics

The depicted image illustrates the structural arrangement of a DNA molecule, specifically pertaining to a chromosome, highlighting the coiling of DNA around histone proteins and identifying the segments of DNA that are deemed accessible ( Label A in the image). 
{: .text-justify}

**Remember: For a cell, accessible regions change according to the stage it is in its cell life cycle. The organ/tissue it is from. The stimuli the cell is receiving**
{: .notice--danger}
<hr>
# Why Peak Calling is Important

Now that we understand what it means to be accessible, what are the benefits of the peak calling method, why do researchers do it?. There are many argument that can be made in favour of it, few of these are listed below (ideas in each point is not mutually exclusive): 
{: .text-justify}

1. <u>To find chromatin accessibility</u>: Peak calling helps identifying accessible regions in the genome that regulates proteins. Which may influence gene expression and other cellular functions.
2. <u>To find regulatory elements</u>: To find specific proteins like transcription factors binding sites which influence gene regulation patterns. Where regulatory elements like enhancer and promoter bind. This may help in discerning the biological process of cellular mechanics. 
3. <u>To understand epigenetic modification</u>: Epigenetic modifications, such as DNA methylation and histone modifications, are crucial for gene regulation and cellular differentiation. Peak calling aids in locating regions of the genome that undergo epigenetic modifications. 
{: .text-justify}
<hr>
# Genomic assays for peak calling

There are many techniques that can be used to find these openings or accessible regions of a cell. A non exhaustive list of DNA accessibility techniques:

* ChIP-seq
* DNase-seq
* ATAC-seq
* FAIRE-seq
* MNase-seq
* ChIP-exo

When considering the abundance of techniques available, it naturally prompts the question of which one is the most optimal. It is a constant pursuit to discover a golden bullet solution, yet regrettably, such a definitive approach does not exist. Each technique possesses distinct strengths and weaknesses, a subject deserving of a comprehensive discussion. For further insights, I invite you to explore the contents of this post.
{: .text-justify}

<u>Some of the desirable features of a good assay can be</u>: Ref: [ [1] ]
1. <u>Replication</u>:
    * Biological replication: The process of replicating an experimental protocol on two separate biosamples.
    * Isogenic replicate: It is a biological replicate with samples from the same human donor or model organism strain.
    * Anisogenic replicate: It is a biological replicate with samples from similar tissue derived from different human donors or model organism strains.
    * Technical replication – Two replicates from the same biosample, treated identically for each replicate. 
2. <u>High Read Depth</u>: Read depth, it refers to the number of times a given position in the genome is sequenced or covered by DNA sequencing reads. It represents the average number of times a specific nucleotide base is read during the sequencing process.
3. <u>High read length</u>: Read length, refers to the length of the individual DNA sequences or fragments generated during the sequencing process. It represents the number of nucleotide bases that can be read or sequenced in a single read. Most of the standard Illumina sequencer produce 150 base pairs read length.
4. <u>High library complexity</u>: It refers to the diversity or uniqueness of DNA fragments within a sequencing library. It represents the number of distinct DNA fragments present in the library and serves as a measure of the complexity or richness of the DNA sample being sequenced.
{: .text-justify}
<hr>
# The raw data

Now that the experiment is done and dusted. The outputs are fastq files. Depending on the experiment setting the fastq files can be for single end read or paired end read.
* Single end read: Single-end sequencing involves sequencing DNA fragments from only one end. In this method, the DNA sample is fragmented, and each fragment is sequenced individually from a single direction. This read is not ideal; it may fail to resolve complex genomic structures, repetitive regions, or distinguish between alternative mapping locations for the reads.
* Paired end read: Paired-end sequencing involves sequencing DNA fragments from both ends. In this method, the DNA sample is fragmented, and then sequenced from both ends, generating two separate reads per fragment. 
{: .text-justify}

It is better to have paired end read.
<hr>
# The common denominator pipeline:

Note: Every research lab may follow their own pipeline as various tools are available. There are also standards e.g ENCODE has its own standard pipeline. No one is right or wrong until and unless it is solving the problem at hand correctly.   
{: .notice--danger}

Now that we have the fastq files ( from single or paired end read) we can start the bioinformatic pipeline. 

1.**<u>Quality Matrix</u>**: The first step will be to test the quality of the fastq files. Depending on the replication and technical replication factors one can end up with many fastq files. One can run the tool called [fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) on each of the fastq files to produce a .html file which will have all the quality matrix in it. To process two files two fastq file one can use the command: 
```bash
fastqc -o ~/tmp/data/results/fastqc/ --memory 10000 --threads 10 /path_to_fastq_folder/file_1.fastq /path_to_fastq_folder/file_2.fastq 
```

Note: Quality of a sequence read usually degrades towards the end or starting of the sequence, depending on the experimental setup. If it degrades below a certain level (visualized by the fastqc), write a script to cut those bases out of all the sequences in the fastq file. As shown below.
{: .notice--danger}
![image-center](/assets/images/post_peak_calling.png){: .align-center}

If there is a large number of fastq files, then the corresponding number of quality metric files (fastqc) will also be large. Visualizing each quality metric individually for every fastq file can become challenging. Fortunately, there is a tool called multiQC that allows the consolidation of all fastqc files into a single .html file for comprehensive visualization.
```bash
multiqc /path_to_folder_containing_fasqc_files/
```

2.**<u>Alignment</u>**: Now that good quality fastq files are in hand, can assemble the sequences in the fastq file to a reference genome (be it human, mouse, etc). Let's assume a reference genome is available, then we have many tools to align the sequences to the reference DNA sequences.  

Note: If there is no reference genome available then one has to assemble the sequence de novo. Also for RNA the alignment tools are different e.g. STAR.
{: .notice--danger}

Two most used alignment tools are 
* BWA / BWA-MEM
* Bowtie2

In this post bowtie2 will be used. 

If the fastq files contain sequences derived from human cells, it is necessary to obtain the corresponding human reference genome. The human reference genome can be obtained by accessing the following [link](https://hgdownload.soe.ucsc.edu/downloads.html). This link provides access to reference genomes of various organisms, including humans.Once the suitable reference genome file has been downloaded, it is essential to index the reference genome. This indexing process enables rapid retrieval of specific regions within the reference genome which will help in faster assembly of sequences. The code below use hg19 reference genome and for faster computation uses 16 threads and large memory footprint (everything is dependent on the system you are using)
```bash
bowtie2-build --noauto --large-index --threads 16 --dcv 4096 --bmax 100000000 hg19.fa hg19
```
Now that the reference genome is indexed. we can begin the alignment of the fragments in the fastq files.
```bash
bowtie2 --large-index -p 16 -q --local -x /path_to_reference/hg19 -U /path_to_fastq/nanog_rep1.fastq -S /path_to_output/nanog_rep1_unsorted.sam
```
3.**<u>Processing</u>**: In the above step the fastq file are converted to SAM format. SAM files are a textual file format that holds alignment details of different sequences that have been mapped to reference sequences. The size of the fastq file varies based on factors such as coverage, read length, the number of reads, etc. Similarly, the size of the SAM file can be substantial depending on the characteristics of the associated fastq files. While SAM files are in a human-readable format, they can be converted into BAM files to reduce their size. BAM files retain the same information as SAM files but are stored in a binary file format that is not directly readable by humans. However, BAM files offer the advantage of being smaller and more efficient in terms of storage and processing. Just an excerpt from one of my experiment, the SAM file was 20GB while the corresponding BAM file was 4.5GB. 
* Convert the SAM file to BAM:
```bash
samtools view -h -S -b -@ 16 -o /path_to_output/nanog_rep1_unsorted.bam /path_to_input/nanog_rep1_unsorted.sam
```
BAM files are often accompanied by a BAM index file also known as a BAI file with a similar name.
* Sort the file: For easy access of the data. Can use samtools to sort the bam file, however using sambamba gives us dual functionality. It will produce the sorted file, and an index file will also get generated. 
```bash
sambamba sort -t 4 -o /path_to_output/nanog_rep1_sorted.bam /path_to_input/nanog_rep1_unsorted.bam
```
* Filter: Depending on the assay type of the experiment (ChIP-seq, ATAC-seq, etc), there may be need for filteration. A significant concern when working with ChIP-seq data relates to the presence of multiple mapped reads, where reads can align to multiple locations on the reference genome. While including these multiple mapped reads can enhance the number of usable reads and the sensitivity of peak detection, it can also introduce an elevated risk of false positives. Consequently, it becomes essential to filter our alignment files and retain only the uniquely mapping reads. This filtering step serves to enhance confidence in site discovery and bolster reproducibility of results[ [2] ]. 

Note: For ATAC-seq filter the mitochondrial reads and filter BAM files based on fragment size.
{: .notice--danger}
```bash
sambamba view -h -t 2 -f bam -F "[XS] == null and not unmapped  and not duplicate" nanog_rep2_sorted.bam > nanog_rep2_align.bam
```
{: .text-justify}

# Peak Calling:

The generated BAM file, resulting from the previous procedures, will serve as an input for the peak calling tools. Depending on the assay type the BAM file has to be filtered and blacklisted regions may be removed.

 Several desirable properties contribute to the accuracy, reliability, and reproducibility of the peaks.

* <u>Replication</u>: One such property is having many ( or at least 2) biological replicate (as discussed above). When peaks are called independently on each replicate, the overlapping peaks across the replicates can serve as a reliable reference or ground truth.
* <u>Peak Rescue</u>: It may happen that in one replicate a peak is being called and in the another replicate for the same region the peak is not called. The signal may be small in one of the replicate and is under the statistical significance but in the other replicate a peak is being called. At this point it is at the discretion of the researcher to include or exclude the signal depending on assay type and answers it is seeking.
* <u>Influence of read depth</u>: Occasionally, the binding event may exist, but the peaks remain undetected due to insufficient read coverage.The overlap between two broad feature region (e.g a promoter region) in two replicate may be very low, whereas for a narrow feature region the overlap may be very high between replicates. The reason behind this discrepancy lies in the fact that calling the feature regions in the broad case requires a greater number of reads due to their coverage across a larger portion of the genome. May add those peaks as being called. 
* <u>Control</u>: If a control (also known as input track) exist then it can be use as a background (background noise) against which peak can be called more efficiently. 
{: .text-justify} 

## How does a peak look like?

Depending upon the assay type the peak may look little different but characteristically they are same for a particular region (e.g promoter or enhancer). For ChIP-seq assay the peaks can be bimodal in nature, As shown below: 

![image-center](/assets/images/post_peak_calling_1.jpg){: .align-center}
doi: 10.1371/journal.pone.0011471. 

A comparison of various assay types and their respective profiling capabilities.

![image-center](/assets/images/post_peak_calling_2.png){: .align-center}
https://doi.org/10.1186/1756-8935-7-33

## Peak calling tools

There are many tools available. One can use multiple tools and form a consensus from the output of these tools.

A non exhaustive list of tools:
* MACS (MACS3)
* HOMER
* SPP
* epic2
* haystack_bio

## Calling peaks using MACS3

Now that we have the necessary understanding to call peaks with MACS v3, the following code can be use:
```bash
macs3 callpeak -t /path_to_filtered_bam/filename_final.bam -c /path_to_control/filename_final.bam -f BAM -g mm -n output_file_prefix 2> ~/path_to_logs/some_filename.log
``` 
Few things to notice, in the above code a control file is used. If control file is not available can remove that argument. output_file_prefix is the filename prefix for all the output files. There are many options that can be given to the MACS tool. Please follow their documentation. 

Note: If suppose the number of reads of the control is 40million and the treatment file is 30million then scale back the control sequence.
{: .notice--danger}

## Removing Blacklisted Regions

Dowwnload the blacklist region from this [link](https://github.com/Boyle-Lab/Blacklist/tree/master/lists).

Note: Blacklisted regions correspond to areas in the genome that exhibit artificially elevated signals, typically associated with specific types of repetitive sequences like centromeres, telomeres, and satellite repeats. To address this, the ENCODE and modENCODE consortia have curated comprehensive blacklists for various species and genome versions, encompassing organisms such as humans, mice, worms, and flies. Prior to advancing with subsequent analyses, it is advisable to filter out these blacklisted regions.
{: .text-justify}  
{: .notice--danger}

One of the file produced by the MACS is a file called .narrowPeak. This file is an extension of BED file formats which contains the peak locations together with peak summit, p-value, q-value (statistical properties of the peak). To intersect the blacklisted region from the .narrowPeak file bedtools can be used.
```bash
bedtools intersect -v -a filename.narrowPeak -b blaclisted_file.bed > filename_filtered.bed
```

# Differential Binding

The peaks correspond to the sites where bindings can occur. Differential binding is useful in finding out changes in DNA-Protein interaction. A protein binds to a DNA at a particular loci in a certain way, but a different protein may bind the same loci in a different way. This differential nature of proteins binding to a particular stretch of DNA is differential binding. 

As mentioned within this post, the inclusion of replicates significantly enhances the reliability of peak calling outcomes. Nevertheless, a mere two replicates typically prove insufficient for conducting quantitative analyses such as differential binding.

Note: It is common for differentially bound sites to display a degree of binding in all sample groups; however, the rate of binding, which is closely associated with binding affinity, undergoes substantial changes across conditions. How to call different binding sites in such a scenario is difficult to answer. 
{: .text-justify}  
{: .notice--danger}

There are many tools for analyzing differential binding: SICER, MACS2, RSEG, MAnorm, HOMER, MMDiff, PePr.


# Conclusion

Conducting such studies involves multiple intricate steps, each of which encompasses more than a simple input-output interaction with a program or tool. Numerous options need to be evaluated at each stage. For instance, the choice of alignment algorithm can significantly impact the number of identified peaks. Furthermore, the existence of various versions of the same tool further complicates matters. In order to obtain the optimal solution, many researchers develop their own customized pipelines tailored to achieve specific outcomes for a particular assay type. The selection of tools and pipelines can vary depending on the research question posed to the data, and it is advisable to maintain an open-minded approach and explore alternative tools to observe differences. Peak calling can be expanded to address questions about differential binding, enabling comparisons between different groups of cells. Additionally, tools for visualizing peaks exist, but that discussion is reserved for a separate post.
{: .text-justify}  


[1]: https://www.encodeproject.org/data-standards/terms/
[2]: https://github.com/hbctraining/Intro-to-ChIPseq-flipped/tree/main/lessons