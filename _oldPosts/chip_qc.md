---
Date: 2013-05-26 14:55
Title: ChIP-Seq: FASTQ data and quality control
Author: Shannan Ho Sui & Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
Tags: galaxy, chip-seq

---

---

We will ultimately be comparing the binding profiles of two transcription factors, Nanog and Pou5f1 (Oct4) from the [HAIB TFBS ENCODE collection](http://hgdownload.cse.ucsc.edu/goldenpath/hg19/encodeDCC/wgEncodeHaibTfbs/) that have been ChIP-sequenced with Illumina in h1-ESC cells. Do look up the transcription factor (TF) information if you are not familiar with them as it should give you an idea what to expect in terms of TF binding.

To keep things manageable and allow algorithms to finish within a few minutes we will work with a single sample (_"h1-hESC - Input replicate 1"_), using reads from 32.8 Mb of chromosome 12 (chr12:1,000,000-33,800,000). We will switch over to using all samples to compare biological replicates and look at differential binding by different transcription factors by retrieving them from the `Shared Data` folders as needed.


### Exploring the FASTQ files

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

While Galaxy has a number of different methods to assess sequence properties you will want to stick to using a standard QC tool such as [FASTQC](http://www.bioinformatics.bbsrc.ac.uk/projects/fastqc/ ) in most cases. 

Under the `NGS: QC and manipulation` tool find `FASTQC: Read QC` and give it a try. 

> What does the quality plot tell you about your data? What additional information do you get with this tool? What can you say about the per-base GC content? Does this match the human genome? Why is there a shift in the GC distribution from the theoretical distribution? Finally, what is the meaning of the k-mer content tab? This publication from [Schroeder et al](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/PLoS%20ONE%202010%20Schr%C3%B6der.pdf) (PDF) has some background information.

Compare your results with a [pre-generated FastQC plot](https://dl.dropboxusercontent.com/u/76426/ChIP-seq/wgEncodeHaibTfbsH1hescRxlchV0422111RawDataRep1_fastqc/fastqc_report.html) obtained from the full FASTQ data set (i.e., using all reads). 

> Do you note any differences in the output or format? Why is that?

Some of the diagnostic plots from a [Core conference call](http://bioinfo-core.org/index.php/9th_Discussion-28_October_2010) might be useful if you are curious to see what different modes of failure frequently look like.

---
**Move on to [Read trimming and filtering](http://scriptogr.am/ohofmann/post/chip-seq-trimming-and-filtering).**


