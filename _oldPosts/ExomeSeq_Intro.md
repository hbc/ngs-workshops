---
Date: 2012-10-11 14:00
Title: Exome-Seq
Author: Oliver Hofmann & John Hutchinson
Contact: ohofmann@hsph.harvard.edu
Type: page
Tags: introduction, galaxy, exome-seq
---

1. [Initial quality control](http://scriptogr.am/ohofmann/post/exome-seq-quality-control)
2. [Read alignment](http://scriptogr.am/ohofmann/post/exome-seq-alignment)
3. [Exome-seq QC](http://scriptogr.am/ohofmann/post/exome-seq-second-qc)
4. [Variant Calling and visual exploration](http://scriptogr.am/ohofmann/post/exome-seq-variant-calling-and-visualization)
5. [Variant annotation](http://scriptogr.am/ohofmann/post/exome-seq-variant-annotation-and-filtering)
6. [Variant prioritization](http://scriptogr.am/ohofmann/post/exome-seq-snp-prioritization)

---

This session provides a basic introduction to conducting a targeted- or exome-seq analysis using the Galaxy framework. 

We will be retracing most of the steps required to get from an Illumina FASTQ sequence file received from a sequencing facility as part of an exome sequencing analysis all the way to variant calls and variant prioritization. To keep things manageable and allow algorithms to finish within a few minutes we picked a single sample and limited reads to those from chromosome 22. Feel free to work through all examples and explore the [reading material](http://scriptogr.am/ohofmann/reading). In addition to those links and manuscripts, SeqAnswers has a useful [short guide](http://seqanswers.com/wiki/How-to/exome_analysis#A_short_guide_to_Exome_sequencing_analysis_using_Illumina_technology) to Exome-seq analysis using the command line which helps when dealing with many samples.

Before tackling the modules below you should have a [working knowledge of Galaxy](http://scriptogr.am/ohofmann/intro-to-galaxy), understand how to find relevant tools, annotate your history or get new data sets from the data library.  As a result we will minimize the screenshots and pointers in these documents, focusing just on _what_ to do while guiding you through the process in class. As always, do ask questions and most importantly collaborate with your fellow students.

In order for you to be able to access Galaxy on your assigned dedicated machine on the Cloud, you have been given a web or IP address in the form of A.B.C.D where A, B, C and D are numbers separated by dots. You will find the current IP address at the top of our [resource page](http://scriptogr.am/ohofmann/resources). You will need it in order to access Galaxy from the web browser on your laptop. 

> If you want to work through this session outside of this course, take a look at our section on [how to set up your own Galaxy server](http://scriptogr.am/ohofmann/post/running-your-own-galaxy) or download the [complete introduction dataset](https://dl.dropbox.com/u/407047/Blog/Data/ExomeSeq.zip) and use one of the public Galaxy instances. Slides used during the session are [available](https://dl.dropbox.com/u/407047/Work/Presentations/20130120%20ExomeSeq%20Course%20Catalyst.pdf) as well.














 






