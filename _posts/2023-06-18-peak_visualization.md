---
layout: single
classes: wide
author_profile: false
sidebar:
  nav: "foo_all"
header:
  overlay_image: /assets/images/post_peak_visualization.jpg
  caption: "(CC) Ralphs_Fotos"
title: "Peak & Coverage Visualization"
excerpt: >
  Peaks represent regions in the genome that exhibit significant signals or enrichment, visualizing peaks can give significant insight into many functional elements.<br />
categories:
  - Genomics
tags:
  - peak calling
  - peak visualization
---

# Peak Visualization

Genomic peak visualization is a vital component of high-throughput sequencing data analysis, particularly in genomics research. Peaks represent regions in the genome that exhibit significant signals or enrichment, often associated with important biological events such as transcription factor binding, histone modifications, or DNA accessibility. 
{: .text-justify}

Visualization is a human process, sometimes what is happening under all this processing is difficult to comprehend. To gain some interpretation about the patterns (motifs), distribution of peaks across the genome visualization is important. Aligning different peak calls from different cell types may help in gaining insight into differentiation of cell types and hence difference in functional elements.
{: .text-justify}

There are many tools to visualize the peaks, one such is UCSC genome browser is an online portal where uploading the peak called files will align the files within each other and also with a reference genome. Similar to this, IGV is another tool that can be downloaded to the local system. Another such local machine tool is IGB.
{: .text-justify}

# Inputs to a visualization tool

Different types of files can be generated from the peak calling tools. Each file contains information about the peaks from a different perspective. Suppose, MACS (MACS3) can generate around 7 files [LINK](https://macs3-project.github.io/MACS/docs/callpeak.html).  Similar files are also produced by other tools, only change is the naming and format. 
{: .text-justify}

* A mental exercise of what information may be needed for visualization.

1. File-A: This file should contain information like range of the peak, start and end location. It may also contain the summit or the location where the peak is highest. It may contain other statistical values of the peak.
2. File-B: The peaks values are usually discrete, to visualize better with reference to the reference genome it is better to have continuous values. Where there are no peaks it can be represented by zero, but values are there.
3. File-C: Peaks can be very large, it will be better if there is a file that contains information about a range where the average peak height is highest for that range. May help in motif discovery.  
{: .text-justify}


In MACS File-A will be NAME_peaks.narrowPeak, File-B will be NAME_peaks.narrowPeak and File-C is NAME_summits.bed, where NAME is the input file name. To visualize, a file has to be uploaded or added into the tool, this is known as creating a track. The tool may be initialized with a reference genome track (not necessary). Shown below is a snippet of peak visualization using IGV. 
{: .text-justify}

![IGV Peak Visualizatio](/assets/images/post_peak_visualization_2.jpg)

## More about BiGWig file.

First we have to understand the wiggle file. This format allows the display of continuous data. The representation in this format is not compressed, the information needs to be compressed first. After the compression it is converted into an indexed binary format. This format is called BigWig format. The representation is similar to another file format used to represent continuous data that is BedGraph. The size of BedGraph is little more than BigWig, but BedGraph is supported in UCSC genome browser. IGV can use BigWig. 
{: .text-justify}

# Another way to visualize peaks

In the preceding section, we presented visualizations of called peaks. However, if one desires to examine the peaks or coverage of the entire dataset without performing peak calling, a profile graph of the entire dataset can be generated. This approach proves beneficial when individuals prefer to identify peaks by directly analyzing the raw data instead of relying on peak calling tools.
{: .text-justify}

**<u>How to create coverage profile of a BAM file?.</u>**

The input is the alignment file BAM. An index file of the BAM is required. Sambamba can be used to sort and index a bam file in one step [command](/genomics/peak_calling/#the-common-denominator-pipeline). Samtool can also do it but at first sort it and then index it. Depending on the assay type there are many tools to create a coverage profile for the indexed BAM file. If the assay is of ChIP-seq then [DeepTools](https://deeptools.readthedocs.io/en/develop/) can be used.DeepTools offers versatile functionality beyond the analysis of ChIP-seq data. While its original implementation demonstrates promising results for ChIP-seq, it can be effectively applied to various other assay types as well.
{: .text-justify}

Another way to create coverage track for assay types such as ChIP-exo/nexus/seq, DNase-seq is a two fold process. First convert the BAM into a bedGraph using [bedtools](https://bedtools.readthedocs.io/en/latest/content/tools/genomecov.html) then convert the bedGraph to BigWig using [bedGraphToBigwig](http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/bedGraphToBigWig) 
{: .text-justify}

Convert BAM to BigWig 

* Approach-1: Using bamCoverage from DeepTools

```bash
bamCoverage -b /path_to_bam/filename.bam -o /path_to_output/output_filename.bw --binSize 20 --numberOfProcessors 16
```
To have a very high spatial resolution the output profile should be equal to the input resolution, for that make <code> --binSize 1 </code>. Making <code> --binSize </code> larger than 1 will average the adjacent bases into a single value. If there is a control file also and want to find out the profile with respect to to control that can also be done, for that use bamCompare.


```bash
bamCompare -b1 /path_to_bam/filename.bam -b2 /path_to_control/control_filename.bam -o /path_to_output/output_filename.bw --binSize 20 --numberOfProcessors 16
```

* Approach-2: A two step process

Conversion of BAM to bedGraph

```bash
bedtools genomecov -ibam input.bam -bga | bedtools merge -i - > covered.bed
```
The command will produce a high spatial resolution profile similar to the resolution of the input. After the bedGraph file is produced, convert it into a BigWig file.
```bash
bedGraphToBigWig input.bedGraph chrom.sizes output.bw
```


Here the chrom.sizes is a path to a file which contains the chromosomes size. Chromosomes size file can be downloaded from [here](https://hgdownload.soe.ucsc.edu/goldenPath), for example for reference genome hg38 it can be downloaded from [here](https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.chrom.sizes). 


# Global characterization

The visualization that has been focused upto now was about presenting snapshots of an individual loci. However, there are methods available that can capture the comprehensive global patterns in terms of each locus. Regulatory elements like promoters, enhancers, silencer and operators commonly known altogether as cis-regulatory elements can be close to the Transcription Start Site (TSS). To visualize the global view of enrichment near TSSs, deepTools can be used. 
{: .text-justify}

Suppose the experiment is to find the activity of a certain (NANOG or CTCF, etc) transcription factor (TF) on all the genes. To visualize its enrichment around TSS, a profile plot that evaluates read density across all start sites needs to be created. The next question is how much further to look on the flanking sides. Considering TSS of a gene as a reference point, one can look at a +/- 4000bp window from this reference to visualize enrichment around this point. 
{: .text-justify}

```bash
computeMatrix reference-point --referencePoint TSS -b 4000 -a 4000 -R /path_to_bed/filename.bed -S /path_to_replicate_bigWig/replicate1.bw /path_to_replicate_bigWig/replicate2.bw --skipZeros -o /path_to_output/matrix_TSS.gz -p 8 
```

The <code> -R </code> provides a path to file or files containing the regions to plot, usually in BED or GTF format. These files will contain information about the genes, its location and other gene structure. The <code> -S </code> contains a single or multiple bigWig files to consider. 

This will only create a file that contains the count of read depth calculated from BigWig around the reference point with a certain window size. In the example given above two bigWig files from two replicates are considered. Next the matrix file is fed into the plot function.
{: .text-justify}

```bash
plotProfile -m /path_to_input_matrix/matrix_TSS.gz -out /path_to_output/TSS_profile.png --perGroup --colors red blue --plotTitle "" --samplesLabel "ko_r1" "ko_r2" --refPointLabel "TSS" -z ""
```
The output will be an image. As shown below the enrichment near TSS is greater for replicate-2.
* x-axis is the window size here 4K base pairs. 
* Y-axis is log2 ratio of the normalized read coverage of the TF divided by the input. (In the image given below the y-axis is scaled quite a bit more than necessary, hence the not up to par look.)

![Matrix Plot](/assets/images/post_peak_visualization_3.jpg)

The heatmap from the same matrix is:

![Heatmap Plot](/assets/images/post_peak_visualization_5.jpg)


## Relationship between a TF and genes

In the context of investigating the potential relationship between a specific transcription factor (TF) and gene regulation, a global plot can be generated to provide a comprehensive visualization of TF binding across all genes. This plot, known as a profile plot, considers the read density associated with the TF across the entirety of the gene in the genome. This can be done by the same procedure as described above, at first create a matrix with <code> computeMatrix </code> and then plot the count matrix. This time the parameter <code> -R </code> will point to a file containing the coordinates of all the known genes in the genome of the sample.
{: .text-justify}
```bash
computeMatrix reference-point --referencePoint TSS -b 4000 -a 4000 -R /path_to_all_known_genes/filename.bed -S /path_to_replicate_bigWig/replicate1.bw /path_to_replicate_bigWig/replicate2.bw --skipZeros -o /path_to_output/matrix_TSS.gz -p 8
```

After the matrix has been created, time to create a profile plot.

```bash
plotProfile -m /path_to_input_matrix/matrix_TSS.gz -out /path_to_output/TSS_profile.png --perGroup --colors blue red --plotTitle "" --samplesLabel "wt_r1" "wt_r2" --refPointLabel "TSS" --yMax 12
```

As seen from the image there is very little enrichment around TSS of all known gene sites. This may not be that bad since the TF has binding sites around a few genes after all!!.

![profile Plot](/assets/images/post_peak_visualization_4.jpg)

## Finding Friends to validate a TF

Upon observing the profile plot, it becomes evident that the TF exhibits binding to only a limited number of genes. Activation of a gene typically requires the involvement of multiple cis-regulatory elements. To bolster the findings, it would be highly advantageous to discover additional evidence supporting the role of this TF. This exercise utilized a publicly available dataset from ENCODE. It is possible to conduct searches for similar experiments conducted on biosamples of the same organ and cell type, at comparable stages in their life cycles. Fortunately, there are other experiments available for this purpose. Although these similar experiments may focus on different assays, such as histone modification, they can contribute valuable insights to the overall investigation. After finding those experiments download the bigWig files associated with it. Remember, download only those files whose reference genome is similar to the reference genome used to create the TF under consideration. In this exercise three different target assays were downloaded, those are for 
* H3K27ac, H3K27me3, H3K4me1.  
{: .text-justify}

![profile Plot with friends](/assets/images/post_peak_visualization_6.jpg)

Thus, **Represor H3K27me3 is not active near the TF under consideration. H3K27ac and H3K4me1 which are known to be an active enhancer are near the TF.**

# Conclusion

