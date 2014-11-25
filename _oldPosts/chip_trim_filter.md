---
Date: 2013-05-26 14:50
Title: ChIP-Seq: Trimming and filtering
Author: Shannan Ho Sui & Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
Tags: galaxy, chip-seq
---

---

## Read trimming and filtering

Depending on your FASTQ results you may need to test for contamination (either by vector or other sourcers) and/or remove adapter sequences from your read prior to alignment. It is good to remove these sequences to increase your mapping efficiency. Note that this is not a problem for our sample data.

## Screen for contamination

Not all required tools are available through Galaxy just yet. For example, depending on the source of your data you probably want to screen your reads for contamination using tools such as [ContEst](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/Bioinformatics%202011%20Cibulskis.pdf) (PDF) or [SeqTrim](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/BMC%20Bioinformatics%202010%20Falgueras.pdf) (PDF). For now we will just explore how you can spot potential contamination from the FastQC results alone. 

> What is the most overrepresented sequence in the pre-generated FastQC results from the h1-hESC sample?

Compare your own FastQC results with a different [pre-generated FastQC summary](http://dl.dropbox.com/u/4253254/Training/HSCI_Workshop/D19VHACXX_s1_0_illumina12index_12_SL17357_fastqc/fastqc_report.html) that highlights a potential problem.

> Study the report. Is there any vector contamination present? Is there any adapter contamination present?

As an emergency solution to remove contaminating sequences, Galaxy comes with a way to `Clip adapter sequences`. If you notice a particularly strong contamination with a vector or primer you can use your FASTQ file as the `Library to clip`, keep the default `Minimum sequence length`, and enter the sequence you spotted in the FASTQC report as the `Adapter` to clip. You probably want to keep both clipped and unclipped sequences in this case; keeping only reads that contained an adapter or barcode can be useful if you expect this to be a feature of all valid reads. For command-line use tools such as [cutadapt](https://code.google.com/p/cutadapt/) are more versatile and less labor-intensive to use.
 
Normally, you would take the filtered output and feed it back into Galaxy, but our dataset has very little contamination so we will move on with the original data set. 

## Filter by quality

As we do not plan on using our data to identify genomic variation individual sequencing errors become less of a problem as long as the sequence can be still mapped to the reference genome. Still, you want to filter sequences where the overall quality is just too low. 

After reviewing the quality diagnostics from your FASTQC report, choose an appropriate lower nucleotide quality that you think would be good for this data (for instance, a quality score below 20 means there is more than a 1/100 chance of an incorrect base call). Use this cutoff to filter out low-quality reads from your data with the `Filter By Quality` tool. After you have filtered your data generate another `FASTQC` quality report.

> Do you have an improvement in read quality? What has changed and why? What percentage of reads did you retain at your cutoff?


## Read Trimming

After the general filtering which removes sequence reads of overall low quality it can be a good idea to trim the end of your reads, cutting away nucleotides at the end that are still of low-quality

> Is this necessary in your case? 

Use the `Trim sequences` tool to trim if required. Make sure to name your finalized FASTQ file that has been filtered and improved. You will be using this file in the next section for mapping. Again, tools such as [sickle](https://github.com/najoshi/sickle) provide more flexibility by allowing for adaptive, window-based trimming, but are not yet part of the default Galaxy toolkit.

It might also be helpful to create a new history at this time and copy over your final sequence file. An easy way to do this is through the `History` menu and the `Copy datasets` function which allows you to pick one or more items in your current history, copying them over to a new or existing one. 

---
**Move on to [Alignment and Visualization](http://scriptogr.am/ohofmann/post/chip-seq-alignment-and-visualization).**
