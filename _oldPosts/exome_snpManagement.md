---
Date: 2013-01-16 14:45
Title: Exome-seq: Variant annotation and filtering
Tags: ngs, vcf, dbsnp, hapmap
Author: Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
---

During the this session you will be annotating the variants you identified with known information such as variant calls from the [HapMap project](http://hapmap.ncbi.nlm.nih.gov/) and filter out low-quality calls to improve the chance of reliably identifying functionally relevant variants. If you feel confident do annotate both VCF files and compare the results, alternatively just pick one of the two and limit your analysis to it.

## Annotating a VCF file

You will be using a number of additional files that contain information about known variants (`dbSNP` and data from the `HapMap` project in VCF format). Data is in the `Reference` folder and was retrieved from the [GATK resource bundle](http://gatkforums.broadinstitute.org/discussion/1213/whats-in-the-resource-bundle-and-how-can-i-get-it). Pull in the dbSNP variant information (just the site information) from the reference library. If you are curious why we are using the 'before 129' version, a number of articles from [MassGenomics](http://massgenomics.org/2012/01/the-current-state-of-dbsnp.html) and FinchTalk [here](http://finchtalk.geospiza.com/2011/01/dbsnp-or-is-it.html) and [here](http://finchtalk.geospiza.com/2011/03/flavors-of-snps.html) provide lots of context; in brief, this excludes the majority of variants detected by next-gen sequencing, the majority of which have not have been properly annotated just yet.

* To make the processing easier filter for `chr22` only using the `Filter` tool from the Filter and Sort section* Use the VCFTools `Annotate` function from VCFTools to merge your filtered chr22 dbSNP information with the GATK output. 

Check the new VCF file; the vast majority of variants now have an `rs` identifier in the `ID` column. 

> Look up one or two identifiers in the [dbSNP database](http://www.ncbi.nlm.nih.gov/projects/SNP/) and report on the kind of information that is available.


## Filtering by quality

When trying to identify disease-associated variants it is important to [identify likely false positive (and _false negative_) variants](http://nextgenseq.blogspot.com/2011/06/false-discovery-of-mutations-by.html). One way to exclude low confidence calls is to filter by minimum coverage and quality of the call, testing to make sure variants are found on reads from both strands and not always at the same read position -- indicating a read duplication problem -- and for non-cancer sample an allele frequency close to 50% or 100%, at least at positions with reasonable read coverage.

### Visually exploring quality metrics

The aligner and variant caller end up adding a [large number of quality metrics](http://gatkforums.broadinstitute.org/discussion/49/using-variant-annotator) to your VCF file, and it can be a bit daunting to evaluate differences between individual samples or slightly different versions of your workflow (such as picking one aligner over the other).

One approach to identify systematic differences between multiple VCF files is to use the [o8 variant visualizer](http://variantviz.rc.fas.harvard.edu/):

* Visit the website and log in using a guest account created for this tutorial: user `hsph_exome`, password `hsph_catalyst`
* Normally you would upload your VCF file and wait for o8 to process and display your data. To keep things simple we have provided two VCF calls from the same sample (lane 8) -- one aligned with Bowtie, one with Bowtie 2, but otherwise treated identically
* Use the `VCF files` selector and add the two VCF files to your active display
* You can now check for systematic differences using a number of different metrics (both in the main display, as well as by fixing additional metrics using the little chart symbol in the metric list on the right)
* You can also use 'categorial' information to test for systematic differences in known or novel variants using the `Categories` switch on the top right, and subsetting to known SNPs (1000 genomes, dbSNP, etc.)

Note:

* the differences in mapping quality (`MQ`)
* how different the `Qual` distribution looks for calls with high or low read depth `DP`
* that Bowtie has a larger number of `unique` variant calls
* this is related to the number of InDels detected in both sets: none for Bowtie -- which does not allow gaps during alignment. As a result, subsequent variant calls close to insertions and deletions are biased towards false-positive calls

For larger data sets these visual reviews can be helpful, in particular when you can subdivide your variant calls in some way -- for example by splitting them in likely true positive and false positive subsets based on concordance with a SNP-chip.

### Manual filtering

Time to switch back to Galaxy. For our data we will be are using somewhat strict criteria this time around to keep the number of variants low; take a look at the [GATK recommendations](http://gatkforums.broadinstitute.org/discussion/1186/best-practice-variant-detection-with-the-gatk-v4-for-release-2-0) again, in particular the "Recommendations for very small data sets" section. Given enough variants and sequence information optimal parameters can be learned by comparing calls against known variant data (dbSNP, 1000 Genomes, etc.) in a process called ["variant score recalibration"](http://www.broadinstitute.org/gatk/gatkdocs/org_broadinstitute_sting_gatk_walkers_variantrecalibration_VariantRecalibrator.html) (VQSR, also see base quality recalibration), but for targeted sequencing experiment there is just not enough information to train on. 

* For now, use a simplified approach via the `Filter` method from VCFTools and set: `Filter by Quality` to 60, Filter `QD 5 lt`, Filter `HRun 5 gt`

 > What do those terms mean?

The `Filter` tool only adds a new column to the VCF file that lists whether a given variant _failed_ or _passed_ the criteria. You can use the _generic_ `Filter` tool to keep lines where `column 7` states `PASS`, but this gets rid of the VCF header information. It can be useful to quickly check how many reads pass the quality control step, though.

> How many variants are left?


### Finding novel variants

Assume we are only interested in 'novel' mutations. Repeat the generic filter, this time removing anything with an `rs` identifier (a known dbSNP mutation) in the `REF` column (`column 3`). 

> How many novel variants are there? Write down one or two positions for later.

As before, send your BAM file and the VCF file to IGV (suggested: the annotated VCF file with the 'PASS' information included).

> Explore one or two of the novel variants you wrote down from your manually filtered file. Are they real? If they have poor support, i.e., only 2-3 reads, go back to the VCF file and find novel entries with a reasonably high number in the `DP` column, then go back to IGV and inspect the position.
