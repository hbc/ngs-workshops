---
Date: 2013-01-16 14:50
Title: Exome-seq: Variant calling and visualization
Tags: ngs, vcf, igv
Author: Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
---

During this session you will take your BAM alignment files, call variants, check for basic annotation and compare the called variants to the original alignment using the Broad’s Integrated Genome Viewer, IGV.

## Background

For a full data set we would be following the Broad's [Best Practice Variant Detection with the GATK](http://gatkforums.broadinstitute.org/discussion/1186/best-practice-variant-detection-with-the-gatk-v4-for-release-2-0), currently at version 4. In particular, we would:

* [Re-align reads](http://www.broadinstitute.org/gsa/wiki/index.php/Local_realignment_around_indels) around insertions and deletions
* [Recalibrate](http://www.broadinstitute.org/gsa/wiki/index.php/Base_quality_score_recalibration) the base quality score
* and mark duplicate reads

Re-alignment is a very time consuming step and we will skip it during this stage. We also cannot reliably re-calibrate base qualities as we only have sequence data for a tiny fraction of the genome (and hence known variants) -- about 2% of chromosome 22, but the process analyzes covariation among nucleotide features such as the reported quality score, the position within the read and the preceding and current nucleotide (sequencing chemistry effect).

It is useful though to at least browse through the reference guidelines to get a basic understanding of what constitutes best practice and _why_.


## Calling Variants

*  Start by pulling in the two previously generated BAM files from your history, or use the pre-generated alignments in the Data Library. We will also need the chr22.fa reference again, and it might be useful to keep the bait region information around for when you are exploring your results.

The `Unified Genotyper` calculates [genotype likelihoods](http://www.broadinstitute.org/gsa/wiki/index.php/Unified_genotyper) using a Bayesian model, and the mathematical model is well explained both in the documentation and associated manuscripts. For a shorter introduction take a look at this [recent presentation from the Broad Workshop Series](https://dl.dropbox.com/u/407047/Blog/Documents/Broad_WS_GATK.pdf). There are a number of ways to tweak its parameters and expectations, for example to handle extremely low or high sequence coverage scenarios, but for now we will rely on the default settings.

The Genotyper requires additional information to be present in the header of your SAM/BAM file before it can call variants. Set these headers using the `Add or replace groups on data` from the Picard section. This includes:

* giving the data a unique identifier, 
* providing information on the sequencing technology, and
* filling out the remaining fields

Take a look at the help section to figure out what the fields mean and what you should enter.

Next, run the `Unified Genotyper` on your modified BAM files. Explore the generated logfile to get some basic information, then take a look at the actual results and try to make sense of one or two entries (i.e., learn about the [information contained in an VCF file](http://www.1000genomes.org/node/101)).


## Comparing SNP calls and alignments

Let's visualize the data. Send one of the two original BAM alignment files (imported right at the beginning) to IGV ('web'). This will either directly launch the [Integrative Genomics Viewer](http://www.broadinstitute.org/igv/) using Java Webstart, or result in an `*.jnlp` being downloaded to your local drive; double-clicking on it should launch the browser with your chosen BAM file. Be patient, the startup might take a few seconds.

When the browser is done loading you will most likely not see any individual reads since you are zoomed out too much. Switch to `chr22` by using the search box or the drop-down selector next to it, then zoom into a gene region. Alternatively, pick the gene name of the bait test file and use that to jump to a region of interest. Hover the mouse over some reads to get additional information, and note how mismatches between the reads and the reference genome are color coded.

IGV knows about the correct reference genome since the information is encoded in your BAM file; it also pre-loaded a list of RefSeq gene definitions, although you can always add more (`Load from Server` under the `File` menu, for example the UCSC gene definitions). Take a look at the gene `BCL2L13`. Explore the coverage at the first exon. 

> Go further upstream to `ATP6V1E1` -- what happened to this gene? 

Convert the bait interval file in your history to BED format (`Edit Attributes`, `Convert to new format`, download the BED file from Galaxy to your desktop and import it into IGV using `File` - `Import from file`. 

> Does the read distribution across the first exon of BCL2L13 and ATP6V1E1 make sense now?

Finally, go back to Galaxy and send the VCF file matching your BAM file to the browser, as well as the second set of BAM/VCF files. Explore the tracks, zooming in on some called variants and compare them to the underlying read distribution. 

> Can you spot differences between the two BAM tracks? Those are caused by the different alignment algorithms as you used the same filtered FASTQ files.

Check for good matches between variant calls and the reads. Try to find homozygous and heterozygous variants, and check for cases where the reads indicate a difference to the reference genome, but no variant was called.

During the next session we will annotate the VCF file and use this annotation to select a small number of high-confidence, novel variants that might be of interest.


