---
Date: 2013-01-16 14:55
Title: Exome-seq: Second QC
Tags: ngs, qc
Author: Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
---

Exome-sequencing is based on a [target-enrichment strategy](http://en.wikipedia.org/wiki/Exome_sequencing#Target-enrichment_strategies) which -- among other approaches -- can be PCR-based or use a [hybrid-capture method](http://www.nature.com/nbt/journal/v29/n10/full/nbt.1975.html?WT.ec_id=NBT-201110) using molecular probes (baits) binding to regions of interest (targets) which are then subsequently sequenced.

As a result, a second quality control step after the alignment has finished can be useful to test just how well the target-enrichment process actually worked. Did the target capture approach enrich for the baited genomic region, i.e., are the targeted region enriched for aligned reads compared to non-targeted region? What is the average coverage? These will give you a rough idea how successful your experiment was and inform downstream filtering choices.

If you are wondering what 'successful' means in this context it might be useful to browse through the [special issue on exome sequencing](http://genomebiology.com/content/12/9) by Genome Biology. One of the best ways to figure out sensible evaluation and filtering strategies is to learn from successful studies. Another excellent and current step-by-step workflow can also be found on the [SeqAnswers wiki](http://seqanswers.com/wiki/How-to/exome_analysis). 

## Exploring bait information

We have uploaded a sample region as 'hg19_bait_test.bed' to the `Exome information` folder of the data library. First task, pull the bait test coordinates into the active history. 

> What region/gene does the bait test overlap? 

This can be done by pulling in all genes (or all genes on chr22) from UCSC into the history and using the operations on genomic intervals to check what it intersects with. The intersect tool depends on the order of input data. Try both versions and compare the different results. 

> How do they differ? 

Send the intersection result that includes the bait information to the UCSC Genome Browser. 

> What is the _name_ (gene symbol) of the gene that the bait region overlaps? 

## Comparison of bait and target regions

The complete target and bait information for chromosome 22 is also in the data library; retrieve the `hg19_chr22_baits.bed` and `hg19_chr22_targets.bed` files into your active history. The targets file contains genomic intervals of exons that we are _aiming_ to capture (enrich for). The baits file contains genomic intervals of those genomic regions that we can actually capture experimentally using the chosen target capture technology.

> Explore the target BED file and the bait BED file manually. How do the coordinates relate to each other?

Send the target/bait BED data (`hg19_chr22_baits.bed` and `hg19_chr22_targets.bed`) to the UCSC Genome Browser for visualization. You will once again want to utilize the `Build custom track` functionality to ensure you can see both coordinate sets at the same time. > Get a sense of how well the targets align with genes and exons.

## Manual review of alignment resultsAdd the alignment results (`BAM` format) to the current history, either from your own alignment or the alignments pre-generated for you. If you have generated your own BAM files and used the `chr22.fa` file as a reference you might still have to tell Galaxy about the genome built you used: edit the attributes of your BAM file and set the genome build to `hg19`.
 
Explore the data and coverage by sending one of your BAM files (aligned with Bowtie or Bowtie2) to UCSC as well . The viewer should remember the bait and target region information you sent previously. 

> How uniform is the coverage for this region? Can you spot regions where there are variants (red lines)? 

Revisit the bait test region you sent to the browser at the start of the session by typing in the gene's name into the search box and jumping to the appropriate coordinates. Is there a variant in this gene based on the BAM file(s) you used? 

> Provide coordinates and the substitution, if any. 
## Enrichment statistics

We will now explore the full target/bait information to your sequence alignment to get a sense of target enrichment, coverage and initial variation information. A simple way to do this is via Picard (`SAM/BAM Hybrid Selection Metrics`)

> What do the metrics tell you about the efficiency and coverage of our exome capture experiment? 

More extensive reports can be generated through other tools such as [TEQC](http://www.bioconductor.org/packages/devel/bioc/html/TEQC.html) from the [BioConductor](http://www.bioconductor.org/) framework. The project website has a sample PDF of the [exome sequencing quality control](https://dl.dropbox.com/u/407047/Blog/Exome%20QC/exomeControl.pdf); there's also a second QC report from a [targeted sequencing study](https://dl.dropbox.com/u/407047/Work/Christiani/LungCancer/Sample1002/teqc.html) with much higher coverage.

> Take a look at the first TEQC report. You should note one region without coverage in the abbreviated coverage table. Can you identify the gene this bait region belongs to?
