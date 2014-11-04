---
Date: 2012-10-11 14:59
Title: ChIP-Seq
Author: Shannan Ho Sui & Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: page
Tags: introduction, galaxy, chip-seq
---

1. [FASTQ data and quality control](http://scriptogr.am/ohofmann/post/chip-seq-fastq-data-and-quality-control)
2. [Read trimming and filtering](http://scriptogr.am/ohofmann/post/chip-seq-trimming-and-filtering)
3. [Alignment and Visualization](http://scriptogr.am/ohofmann/post/chip-seq-alignment-and-visualization)
4. [Peak calling](http://scriptogr.am/ohofmann/post/chip-seq-peak-calling)
5. [Motif detection and functional enrichment](http://scriptogr.am/ohofmann/post/chip-seq-enrichment-analysis)

---

This session provides a basic introduction to conducting a ChIP-seq analysis using the Galaxy framework. Some material has been borrowed [Morgane Thomas-Chollier’s ChIP-seq tutorial](http://ngs.molgen.mpg.de/ngsuploads/Cornelius/ESGI/Chip.htm) and [Galaxy workflow](http://main.g2.bx.psu.edu/u/morgane/h/fromreadstopeaks), and the [Princeton HTSEQ Users Tutorial](https://sites.google.com/site/princetonhtseq/tutorials/chip-seq). 

We will be retracing most of the steps required to get from an Illumina FASTQ sequence file received from a sequencing facility as part of an ChIP sequencing analysis all the way to performing peak calling and identifying over represented sequence motifs and functional annotations. We will focus on the following steps: initial quality control, read mapping, peak calling, identification of over represented seqeuence motifs, annotation of regions with genes, and functional enrichment analysis of the peaks. Feel free to work through all examples and explore the reading material.

The default Galaxy instance relies on [MACS](http://liulab.dfci.harvard.edu/MACS/) for peak calls. Several other peak calling algorithms are also available in Galaxy; e.g., [SICER](http://home.gwu.edu/~wpeng/Software.htm) has been specifically designed to for analysis of histone modifications and is available through the [Galaxy Toolshed](http://toolshed.g2.bx.psu.edu/). For this exercise, we will use MACS to identify ChIP-seq peaks for two transcription factors and compare the results.

Before tackling the modules below you should have a [working knowledge of Galaxy](http://scriptogr.am/ohofmann/intro-to-galaxy), understand how to find relevant tools, annotate your history or get new data sets from the data library.  As a result we will minimize the screenshots and pointers in these documents, focusing just on _what_ to do while guiding you through the process in class. As always, do ask questions and most importantly collaborate with your fellow students.

In order for you to be able to access Galaxy on your assigned dedicated machine on the Cloud, you have been given a web or IP address in the form of A.B.C.D where A, B, C and D are numbers separated by dots. You will find the current IP address at the top of our [resource page](http://scriptogr.am/ohofmann/resources). You will need it in order to access Galaxy from the web browser on your laptop. 

> If you want to work through this session outside of this course, take a look at our section on [how to set up your own Galaxy server](http://scriptogr.am/ohofmann/post/running-your-own-galaxy) or download the [complete introduction dataset](https://dl.dropboxusercontent.com/u/407047/Blog/Data/ChIP-Seq%20Data.zip) and use one of the public Galaxy instances.


---
**Move on to [FASTQ data and quality control](http://scriptogr.am/ohofmann/post/chip-seq-fastq-data-and-quality-control).**








 






