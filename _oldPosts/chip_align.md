---
Date: 2013-05-26 14:45
Title: ChIP-Seq: Alignment and visualization
Author: Shannan Ho Sui & Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
Tags: galaxy, chip-seq, igv, bowtie
---

---

If for some reason any of the previous steps did not work you can retrieve a quality-controlled, trimmed and filtered FASTQ file from the `Data Library` in the `ChIP-Seq Data` library, subfolder `Sequence and reference data` (`H1hesc_Input_Rep1_chr12_qualityfiltered.fastq`).

## Standard alignment

Next we are going to look at the steps we need to take once we have a clean, filtered FASTQ file that is ready for alignment. Use the filtered FASTQ file that you prepared in the previous section. The alignment process consists of the following steps:

* Choose an appropriate reference genome to map your reads against
* Choose an appropriate gene annotation model to guide your alignment
* Perform the read alignment

### Load the filtered FASTQ file and Reference Genome

To avoid excessive runtimes during later steps we will not align the reads against the whole human genome, just `chr12:1,000,000-33,800,000`. We have retrieved the sequence for this chromosome from UCSC GoldenPath (hg19) and added it to the "Data Library". This means we won't use the pre-built genome indices, but submit our own reference sequence. We are also using only a subset of reads from a single sample for the next few steps.

1. Start up a new blank history and give it a name.
2. Either load your filtered FASTQ files from the previous tutorial, or download a filtered FASTQ file from the Shared Data Libraries in Galaxy. 
3. Find the chromosome 12 genomic sequence in the `ChIP-Seq Data` folder as `hg19-chr12-reference_sequence.fa` and import it into your new history.

Using it generates a slight time overhead since the reference genome needs to be indexed prior to each alignment run, but this is acceptable for now.


### Perform Read Alignment

You will start by aligning your reads to chr12 using a standard aligner, `Bowtie`. If you'd like to learn more about its underlying algorithm, advantages and drawbacks a recent [review from Bao et al](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/Exome%20Seq/J%20Hum%20Genet%202011%20Bao.pdf) (PDF) might be of interest. It also references the original paper which walks you through the methods.

You can find the tool under the `NGS:Mapping` tool heading. Make sure you select the corresponding tool for `Illumina`. Do not use the built-in reference genomes, and instead, select `Use one from the history` and choose the `chr12-reference_sequence.fa`. Select `Single-End` under “library mate pairing”. In the Bowtie settings, choose `Full parameter list`. As you can see, there are many parameters that you can change depending on the type of data you are working with. Change the `Suppress all alignments for a read if more than n reportable alignments exist (-m)` from `-1` to `1` to ensure that only uniquely mapping reads are reported. Click the `Execute` button to launch the alignment. [_Note: There's also a Bowtie Version 2 by now, but we'll stick to Bowtie 1 for the time being._]

> While the alignment is running, do [look up the documentation](http://bowtie-bio.sourceforge.net/manual.shtml) to see what the various tool options do. Take a look at the output file. Note it’s size. How long did it take to run? Now extrapolate to how long you would expect this tool to run when mapping to the entire genome (approximately).


### Filter unmapped reads and convert SAM files to BAM files

Most aligners produce output in ["SAM" format](http://samtools.sourceforge.net/) (Sequence Alignment/Map format by now, see [publication from Heng Li](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/Exome%20Seq/Bioinformatics%202009%20Li-3.pdf) (PDF) for more details). 

> Explore the SAM format. What key information is contained?

The SAM formatted output contains all reads along with flags indicating whether they have been mapped or not, their quality values and the genomic coordinates for mapped reads. Filter out the unmapped reads by applying the `Filter SAM` tool under `NGS:SAM Tools`. Click on the `Add a new flag` button. Select `The read is unmapped` under `Type` and set the state for this flag to `No` to discard unmapped reads.

> How many lines are in this final file? This represents the number of aligned reads. Calculate the percentage of aligned reads for this experiment.

Another common preprocessing step for NGS data is to filter out duplicates. For ChIP-Seq data, these can be the result of a genuine signal or can be caused by PCR amplification artifacts, especially at high sequencing depth. Duplicates that result from ChIP enrichment form nice peaks surrounded by an otherwise more even distribution of reads. In general, the recommendation is to avoid directly filtering duplicates. MACS handles biases introduced by amplification and library preparation by removing duplicate reads if their count is higher than can be expected from the sequencing depth (binomial distribution with a p-value < 10e-05).

To speed up processing those need to get converted into their binary counterpart (BAM).

* Apply the `SAM-to-BAM` tool under the `NGS:SAM Tools` heading to convert your output SAM file to the compressed BAM format, once again using the chromosome 12 reference sequence from your history as reference


### Explore alignment in a genome browser

Take a look at your alignment in IGV (Integrative Genomics Viewer). To do so, first expand the alignment result (the `BAM` file) in your history and click on the `web current` link beside `display with IGV`. This will download IGV to your machine. It should start automatically after a few security warnings (if not, find the `igv.jlnp` file and click it yourself).

You should see a window that looks like this:

[![IGV Startup](https://dl.dropboxusercontent.com/u/407047/Blog/Screenshots/IGV_Chip_1.png)](https://dl.dropboxusercontent.com/u/407047/Blog/Screenshots/IGV_Chip_1.png)

Click in the highlighted window…

[![Highlight](https://dl.dropboxusercontent.com/u/407047/Blog/Screenshots/IGV_Chip_2.png)](https://dl.dropboxusercontent.com/u/407047/Blog/Screenshots/IGV_Chip_2.png)

… and enter the gene name `AKAP3`. You should now be able to see the individual reads, you can zoom in further using the controls on the upper right and scroll around by clicking and dragging in the highlighted alignment track. Note that IGV automatically translated the gene symbol into the matching genomic coordinates for your genome build:

[![Sample Gene](https://dl.dropboxusercontent.com/u/407047/Blog/Screenshots/IGV_Chip_3.png)](https://dl.dropboxusercontent.com/u/407047/Blog/Screenshots/IGV_Chip_3.png)

Recall that this is the input file, i.e. the control.

> Can you identify any potential regions of enrichment in this gene or others? 

ChIP-seq data is not distributed evenly across the genome and, even in the input sample, you will see clustering of reads around gene regions and especially around promoter areas, which is why we need the input/control sample. By comparing the number and distribution of reads between input and your sample, you essentially correct for this background read distribution. 

Let's compare the input and the corresponding Nanog TF ChIP-Seq data side by side, and this will be immediately apparent. 

* Go to `Shared Data`, `Data Libraries`, open the `ChIP-Seq Data` folder, then open the `Additional Sample data` folder.  Find the Nanog alignment data `H1hesc_Nanog_Rep1_chr12_aln.bam` and import it into your current history.

Expand the alignment result (the `BAM` file) in your history by clicking on the file name and then click on the `local` link beside `display with IGV`. This will automatically download the alignment file into the IGV window that is already open so you can compare the two alignment files.

> Can you identify any potential Nanog binding sites based on the comparison of the input vs. Nanog ChIP results?

---
**Move on to [Peak calling](http://scriptogr.am/ohofmann/post/chip-seq-peak-calling).**


