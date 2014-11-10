---
Date: 2013-01-16 15:00
Title: Exome-seq: Alignment
Tags: ngs, alignment
Author: Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
------

## Exome Sequencing and Alignment

Next we are going to look at the steps we need to take once we have a clean, filtered FASTQ file that is ready for alignment. You can either use the filtered FASTQ file that you prepared in the previous section, or download a new one from the Shared Data Libraries in Galaxy (the `*clean.fastq` files in the `Snapshots` folder, making sure you pick the same lane as before). The alignment process consists of the following steps:

* Choose an appropriate reference genome to map your reads against* Perform the read alignment using one of several alignment tools such as Bowtie, Mosaik or BWA, creating an output SAM file. For the purposes of this tutorial we recommend you align your reads using different aligners and -- keeping all other steps identical -- compare the resulting variant calls at the end of the session* Convert the SAM file(s) to compressed BAM format* Generate BAM index statistics* Perform quality control on the exome enrichment 

## Load the filtered FASTQ file and Reference Genome

* Start up a new blank history and give it a name.*  to  "Either load your filtered FASTQ files from the previous step using “Copy Datasets, or download a filtered FASTQ file from the Shared Data Libraries in Galaxy. Make sure the Lane matches the one that you worked on in the previous tutorial.
* To avoid excessive runtimes during later steps we are not aligning the sequences against the whole human genome, just `chr22`. This means we are not using the pre-built genome indices, but submit our own reference sequence. We have retrieved the sequence for this chromosome from UCSC GoldenPath (hg19) and added it as `chr22.fa` to the `chr22` folder in the Exome-Seq Sharded Data library from where you should import it into your new history.

## Perform Read Alignment

You will be aligning your reads to chr22 using two standard aligners, `Bowtie` and `Bowtie2`. If you'd like to learn more about their underlying algorithms, advantages and drawback a recent [review from Bao et al](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/Exome%20Seq/J%20Hum%20Genet%202011%20Bao.pdf) (PDF) might be of interest. It also references the original papers which walk you through the methods.

You can find these tools under the `NGS:Mapping` tool heading. Make sure you select the corresponding tool for `Illumina`. Select `Single-End` under “library mate pairing” and perform the mapping using default options (Bowtie); the same applies to Bowtie2. 

Remember **not** to use the built-in reference genomes, picking the `chr22.fa` file from your history instead. This generated a slight overhead since the reference genome needs to be indexed prior to each alignment run, but this is acceptable for now. 

> Look up the documentation to see what the various tool options do. Take a look at the output file. Note it’s size. How long did it take to run? Now extrapolate to how long you would expect this tool to run when mapping to the entire genome (approximately).> Which one was faster? We’ll be comparing the differences between these two alignments later on.## Convert SAM files to BAM files

Most aligners produce output in ["SAM" format](http://samtools.sourceforge.net/) (Sequence Alignment/Map format, see [publication from Heng Li](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/Exome%20Seq/Bioinformatics%202009%20Li-3.pdf) (PDF) for more details). 

> Explore the SAM format. What key information is contained?

To speed up processing those need to get converted into their binary counterpart (BAM).

* Apply the `SAM-to-BAM` tool under the `NGS:SAM Tools` heading to convert your output SAM file(s) to the compressed BAM format* Note how Bowtie2 produced a BAM file straight away. This tends to be the default for newer aligners## Generate BAM Index Statistics
Calculate the index statistics using the `BAM Index Statistics` tool under the `NGS:Picard` tool heading. 

> What kinds of statistics are reported? What do they tell you about the alignment?

