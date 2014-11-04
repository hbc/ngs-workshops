---
Date: 2013-01-16 15:05
Title: Exome-seq: Quality control
Tags: ngs, qc
Author: Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
---

You should have a working knowledge of Galaxy by now, understanding how to find relevant tools, annotate your history or get new data sets from the data library.  As a result we will minimize the screenshots and pointers in these documents, focusing just on _what_ to do while guiding you through the process in class. As always, do ask questions and most importantly collaborate with your fellow students.

## Quality Controls

We will start with the mandatory quality controls after receiving our sequence data from the core facility in [FASTQ format](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/Nucleic%20Acids%20Res%202009%20Cock.pdf) (PDF). The FASTQ file contains output reads from the sequencer that need to be mapped to a reference genome for us to understand where those reads came from on the sequenced genome. However, before we can delve into read mapping, we first need to make sure that our preliminary data is of sufficiently high quality. This involves several steps:

1. Obtaining summary quality statistics on the reads and review diagnostic graphs 2. Eliminate sequencing artifacts3. Filter out genetic contaminants (primers, vectors, adaptors)4. Filter out low-quality reads5. Recalculate quality statistics and review diagnostic plots on filtered data

Iterate through steps 2-5 until the data is of sufficient quality before proceeding to mapping.### Exploring the FASTQ files
Open up Galaxy from your machine as before, start up a new blank history and give it a name. In the top menu, move your mouse cursor over `Shared data` and select `Data libraries`. This allows you to import files into Galaxy that have been shared with you
You will be assigned to analyze one of two sequence files. Browse to that file under `Exome-Seq Data`, folder `chr22` and mouse over the arrow to the right of the filename. In the context menu select `Import to current History`. The file should now appear in your history.

> Take a look at the file contents using Galaxy's preview and file view functionality. How many reads are in your file? What additional information does FASTQ contain over FASTA? Pick the first sequence in your FASTQ file and note the identifier. What is the quality score of it's first and last nucleotide, respectively?### Obtain Quality Statistics

Under the `NGS:QC and manipulation` tool heading, select the `Compute quality statistics` tool (from the `FASTX toolkit` section) and apply it to your FASTQ file. Take a look at the contents of the generated file.

> What do you see? Try to make sense of the various columns

In most cases you will stick to using a standard QC tool such as [FASTQC](http://www.bioinformatics.bbsrc.ac.uk/projects/fastqc/ ). Find it in the Galaxy tool kit and give it a try.

> Do you observe similar quality statistics as before? What additional information do you get with this tool? What can you say about the per-base GC content? Does this match the human genome? Why is there a shift in the GC distribution from the theoretical distribution? Finally, what is the meaning of the k-mer content tab? This publication from [Schroeder et al](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/PLoS%20ONE%202010%20Schr%C3%B6der.pdf) (PDF) has some background information.

Compare your results with either of the two pre-generated FastQC plots at: 

* For [7_100326](https://dl.dropbox.com/u/407047/Blog/QC%20and%20Alignment/7_100326_FC6107FAAXX-chr22_fastqc/fastqc_report.html)
* For [8_100326](https://dl.dropbox.com/u/407047/Blog/QC%20and%20Alignment/8_100326_FC6107FAAXX-chr22_fastqc/fastqc_report.html)

> Do you note any differences in the output or format? Why is that?

Some of the diagnostic plots from a [Core conference call](http://bioinfo-core.org/index.php/9th_Discussion-28_October_2010) might be useful if you are curious to see what different modes of failure frequently look like.

### Screen for contamination

Not all required tools are available through Galaxy just yet. For example, depending on the source of your data you probably want to screen your reads for contamination or vector sequences using tools such as [ContEst](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/Bioinformatics%202011%20Cibulskis.pdf) (PDF) or [SeqTrim](https://dl.dropbox.com/u/407047/Blog/Documents/Literature/QC/BMC%20Bioinformatics%202010%20Falgueras.pdf) (PDF).

It is quite easy to add such tools to your own Galaxy instance, but for now we will just explore SeqTrim using it's web service.

* To limit the load on the SeqTrim servers import the `SampleFASTQ` sequence file from the data library (`Exome-seq data`, `Contamination` folder) into your history. It contains the first 40,000 reads of the full `7_100326` sample
* Download the file to your local harddrive
* Navigate to the [SeqTrim website](http://www.scbi.uma.es/ingebiol/session/new/seqtrimnext) and login as a guest using your email address
* Pick a job name, select `fastq` as format, upload the `SampleFASTQ` file, and pick the `low_quality` trimming pipeline before submitting it to the server

> Study the report. Are there any vector contaminations present? 

Normally, you would take the filtered output and feed it back into Galaxy, but given time considerations we will move on with the original data set. 

As an alternative, Galaxy comes with a way to `Clip adapter sequences`. If you notice a particularly strong contamination with a vector or primer you can use your FASTQ file as the `Library to clip`, keep the default `Minimum sequence length`, and enter the sequence you spotted in the SeqTrim report as the `Adapter` to clip. You probably want to keep both clipped and unclipped sequences in this case; keeping only reads that contained an adapter or barcode is useful if you expect this to be a feature of all valid reads. 

### Filter by quality

After reviewing the quality diagnostics from FASTQC, choose an appropriate lower nucleotide quality that you think would be good for this data. Feel free to use the following tools to filter out low-quality reads from your data: `Filter FASTQ` or `Filter By Quality`. After you have filtered your data generate another `FASTQC` quality report.

> Do you have an improvement in read quality? What has changed and why?


### Read Trimming and Wrap-Up

After the general filtering which removes sequence reads of overall low quality it can be a good idea to trim your reads, cutting away nucleotides at the end that are still of low-quality

> Is this necessary in your case? 

Use the `Trim sequences` tool to trim if required. Make sure to name your finalized FASTQ file that has been filtered and improved. You will be using this file in the next section for mapping.

It might also be helpful to create a new history at this time and copy over your final sequence file. An easy way to do this is through the `History` menu and the `Copy datasets` function which allows you to pick one or more items in your current history, copying them over to a new or existing one. 
