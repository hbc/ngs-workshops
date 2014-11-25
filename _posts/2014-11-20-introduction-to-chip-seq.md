---
layout: post
title: "Introduction to ChIP-Seq"
modified:
categories: courses
excerpt:
tags: [ngs, chip-seq, introduction, galaxy, qc, alignment, peak detection]
image:
  feature:
date: 2014-11-20T01:11:42-04:00
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

This session provides a basic introduction to conducting a ChIP-seq analysis using the Galaxy framework. Some material has been borrowed [Morgane Thomas-Chollier’s ChIP-seq tutorial](http://ngs.molgen.mpg.de/ngsuploads/Cornelius/ESGI/Chip.htm) and [Galaxy workflow](http://main.g2.bx.psu.edu/u/morgane/h/fromreadstopeaks), and the [Princeton HTSEQ Users Tutorial](https://sites.google.com/site/princetonhtseq/tutorials/chip-seq). 

### Course scope
{:.no_toc}

We will be retracing most of the steps required to get from an Illumina FASTQ sequence file received from a sequencing facility as part of an ChIP sequencing analysis all the way to performing peak calling and identifying over represented sequence motifs and functional annotations. We will focus on the following steps: initial quality control, read mapping, peak calling, identification of over represented seqeuence motifs, annotation of regions with genes, and functional enrichment analysis of the peaks. Feel free to work through all examples and explore the reading material.

The default Galaxy instance relies on [MACS](http://liulab.dfci.harvard.edu/MACS/) for peak calls. Several other peak calling algorithms are also available in Galaxy; e.g., [SICER](http://home.gwu.edu/~wpeng/Software.htm) has been specifically designed to for analysis of histone modifications and is available through the [Galaxy Toolshed](http://toolshed.g2.bx.psu.edu/). For this exercise, we will use MACS to identify ChIP-seq peaks for two transcription factors and compare the results.

### Requirements
{:.no_toc}

Before tackling the modules below you should have a [working knowledge of Galaxy]({{ site.baseurl }}/courses/introduction-to-galaxy/), understand how to find relevant tools, annotate your history or get new data sets from the data library.  As a result we will minimize the screenshots and pointers in these documents, focusing just on _what_ to do while guiding you through the process in class. As always, do ask questions and most importantly collaborate with your fellow students.

In order for you to be able to access Galaxy on your assigned dedicated machine on the Cloud, you have been given a web or IP address in the form of A.B.C.D where A, B, C and D are numbers separated by dots. You will find the current IP address at the top of our [resource page]({{ site.baseurl }}/resources). You will need it in order to access Galaxy from the web browser on your laptop. 

> If you want to work through this session outside of this course, take a look at our section on [how to set up your own Galaxy server]({{ site.baseurl }}/courses/running-your-own-galaxy-instance/) or download the [complete introduction dataset](https://dl.dropboxusercontent.com/u/407047/Blog/Data/ChIP-Seq%20Data.zip) and use one of the public Galaxy instances.

## Background

We will ultimately be comparing the binding profiles of two transcription factors, Nanog and Pou5f1 (Oct4) from the [HAIB TFBS ENCODE collection](http://hgdownload.cse.ucsc.edu/goldenpath/hg19/encodeDCC/wgEncodeHaibTfbs/) that have been ChIP-sequenced with Illumina in h1-ESC cells. Do look up the transcription factor (TF) information if you are not familiar with them as it should give you an idea what to expect in terms of TF binding.

To keep things manageable and allow algorithms to finish within a few minutes we will work with a single sample (_"h1-hESC - Input replicate 1"_), using reads from 32.8 Mb of chromosome 12 (chr12:1,000,000-33,800,000). We will switch over to using all samples to compare biological replicates and look at differential binding by different transcription factors by retrieving them from the `Shared Data` folders as needed.


### Exploring the FASTQ files
{:.no_toc}

Open up Galaxy from your machine as before, start up a new blank history and give it a name. In the top menu, move your mouse cursor over `Shared data` and select `Data libraries`. This allows you to import files into Galaxy that have been shared with you.

Browse to the `ChIP-Seq Data` folder, expand the `Sequence and reference data` folder, and click on the arrow to the right of the filename `H1hesc_Input_Rep1_chr12_unfiltered.fastq`. In the context menu select `Import this dataset into selected histories`. On the next screen, select the history you are using. The file should now appear in your history

This is the kind of data you would expect to receive from your sequencing core facility: a large number of short nucleotide reads in [FASTQ format](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/Nucleic%20Acids%20Res%202009%20Cock.pdf) (PDF). 

> Take a look at the file contents using Galaxy's preview and file view functionality. What additional information does FASTQ contain over FASTA? How many reads are in your file? Pick the first sequence in your FASTQ file and note the identifier. What is the quality score of it's first and last nucleotide, respectively?

## Quality Controls

The FASTQ file contains output reads from the sequencer that need to be mapped to a reference genome for us to understand where those reads came from on the sequenced genome. However, before we can delve into read mapping, we first need to make sure that our preliminary data is of sufficiently high quality. This involves several steps:

1. Obtaining summary quality statistics on the reads and review diagnostic graphs 
2. Eliminate sequencing artifacts
3. Filter out genetic contaminants (primers, vectors, adaptors)
4. Filter out low-quality reads
5. Recalculate quality statistics and review diagnostic plots on filtered data

Iterate through steps 2-5 until the data is of sufficient quality before proceeding to mapping.

### Obtain Quality Statistics
{:.no_toc}

While Galaxy has a number of different methods to assess sequence properties you will want to stick to using a standard QC tool such as [FASTQC](http://www.bioinformatics.bbsrc.ac.uk/projects/fastqc/ ) in most cases. 

Under the `NGS: QC and manipulation` tool find `FASTQC: Read QC` and give it a try. 

> What does the quality plot tell you about your data? What additional information do you get with this tool? What can you say about the per-base GC content? Does this match the human genome? Why is there a shift in the GC distribution from the theoretical distribution? Finally, what is the meaning of the k-mer content tab? This publication from [Schroeder et al](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/PLoS%20ONE%202010%20Schr%C3%B6der.pdf) (PDF) has some background information.

Compare your results with a [pre-generated FastQC plot](https://dl.dropboxusercontent.com/u/76426/ChIP-seq/wgEncodeHaibTfbsH1hescRxlchV0422111RawDataRep1_fastqc/fastqc_report.html) obtained from the full FASTQ data set (i.e., using all reads). 

> Do you note any differences in the output or format? Why is that?

Some of the diagnostic plots from a [Core conference call](http://bioinfo-core.org/index.php/9th_Discussion-28_October_2010) might be useful if you are curious to see what different modes of failure frequently look like.



 










