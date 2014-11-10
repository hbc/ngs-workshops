---
Date: 2013-05-26 14:40
Title: ChIP-Seq: Peak calling
Author: Shannan Ho Sui & Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
Tags: galaxy, chip-seq, igv, macs, spp
---

---

As before, if any of the previous steps did not work out you can retrieve intermediate results from the "Snapshot" `Data Library` under "Shared Data". We have deposited the Bowtie-aligned reads in BAM format in the `Additional sample data` library.

The goal of peak calling is to define regions with a high density of reads indicating where the studied factor bound. There are [multiple algorithms to perform the peak-calling](http://www.plosone.org/article/info:doi/10.1371/journal.pone.0011471) step. In this workshop we will be using a tool called MACS.

ChIP signal strength is a continuum with far more weak sites than strong. As a result, the composition of the final peak list depends heavily on the specific parameter settings and algorithm as well as the quality of the experiment itself. Thresholds that are too relaxed lead to a high proportion of false positives for each replicate, but as you will see in the Handling Replicates section, subsequent analysis can remove false positives from a final joint peak determination. 

## Peak calling using MACS

We will use MACS to call "Nanog" peaks in a ChIP (tag) sample versus a control (input) sample. Although MACS can be run without a control data set, an appropriate control is critical for robust analysis of any ChIP-seq experiment because DNA breakage during sonication is not uniform. Some regions of the genome, particularly those at open chromatin, are sheared more readily than others and these fragments can be over-represented in the sequencing step, giving rise to false positive sites of occupancy. The control data set for this study used DNA isolated from cells that were cross-linked and fragmented under the same conditions as the ChIP DNA but without the antibody. This is sometimes referred to as “reverse-cross-linked chromatin” or “Input DNA”. An alternative approach is a “mock IP” in which a control antibody IgG antibody is used that does not recognize any DNA binding protein (“IgG” control). Additional information can be obtained from the [ENCODE/modENCODE ChIP-seq guidelines](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3431496/).

1. Copy the aligned control (input) BAM file and the `H1hesc_Nanog_Rep1_chr12_aln.bam` from the previous section to a new history.
2. Select `MACS` from the `NGS:Peak Calling` menu. 
3. Enter an `Experiment Name` (e.g., _MACS_NanogRep1_)
4. Select the `H1hesc_NanogRep1_chr12_aln.bam` file for the `ChIP-Seq Tag File`, and the `H1hesc_InputRep1_chr12_aln.bam` file for your `ChIP-Seq Control File`.
5. Note the `Effective genome size`, which is the size of the genome that is can be sequenced and mapped (minus telomeres, repeats, etc). Use the default since we are dealing with human data (2,700,000,000). For mouse, the value is 1,870,000,000. For less commonly used species, an estimate of 70-90% of the full genome size is reasonable.
6. Set the `Tag size` to 36bp (based on examining the FastQC report).
7. Note the `Band width` parameter. This value is used to scan the genome for model building. You can set this parameter as the expected sonication fragment size. We will leave it at the default value of 300.
8. Note the `MFOLD` parameter which is used to select genomic regions to build the experiment-specific peak model. A region is used for the model if it contains more than mfold reads than the region surrounding it. We will use the default value (32) but this value can be tweaked to obtain more or less peaks.
9. Check the box for `Perform the new peak detection method (futurefdr)`. This uses both the control and treatment data to calculate local bias and identify peak locations.

While MACS is running, use the time to browse through its [manual](http://liulab.dfci.harvard.edu/MACS/00README.html) or explore the [MACS Protocol paper](https://dl.dropboxusercontent.com/u/76426/ChIP-seq/nprot.2012.101.pdf) (PDF) which describes how to set parameters for transcription factor binding and histone modification data sets, and how to interpret the output. A new version, [MACS2](https://pypi.python.org/pypi/MACS2/2.0.10.20130419), has been released but is not available in this Galaxy instance. 

The algorithm will generate two files. The first output is a BED file with the coordinates of the peaks. Instructions for viewing the peaks in IGV follows below.

> How many peaks (“regions”) were detected by MACS?

The second output is an HTML page that links to the results in various formats and lists the parameters and tasks that were performed. Although warning messages do not affect the success of a MACS run, the majority should still be carefully evaluated. For example, the warning message _'Treatment tags and Control tags are uneven'_ means that the FDR of the resulting peaks will be overestimated when the control sample has more reads and will be underestimated when the ChIP-seq sample is sequenced more deeply. The message _'Fewer paired peaks X than 1,000'_ means that MACS only identified X model peaks and may indicate potential data quality issues because 1,000 model peaks are needed to robustly estimate ChIP-DNA fragment size. The message _'missing chromosome X data'_ might suggest that the raw input file for that chromosome is incomplete. 

Under `Additional Files`, click on the first file ending with `model.pdf`. This file shows the peak model built by MACS. ChIP-Seq DNA fragments are sequenced from the 5’ end, resulting in alignment of tags that form two peaks, on each strand, flanking the location that was bound by the protein of interest. The red curve represents the distribution of reads on the positive strand at each base position, and the blue line models the reads on the negative strand. The black curve is the combined profile that is generated by shifting each distribution toward the center. The detected DNA fragment length is given by d and varies among different ChIP-seq libraries.

> Note that the estimated fragment length (d) is 103 which is much smaller than the default band width parameter of 300 used by MACS. This accounts for the jagged peak model. If you run it again and modify the band width parameter to 100, you will see smooth peaks in the peak model diagram.

The `peaks.xls` file contains all of the information about the peaks identified by MACS, including key parameters, coordinates and enrichment statistics.  

### Visual exploration

We will use IGV again to study some of the results:

1. View the resulting MACS `peaks: bed` file in IGV. As Galaxy does not support automatic export of BED files to IGV, you will have to add it to IGV yourself. To do so, _download_ the file from Galaxy and take note of where you saved it. Now move over to IGV and click the `File` menu and then `Load from file`. Select the file you downloaded and open it in IGV to explore the MACS peak calls next to your Bowtie alignment.
2. Type `Akap3` in the coordinate text box to zoom in on this region and observe the correlation between the MACS peak call and the alignment. Another interesting gene to look at is `Sox5`.


## Handling replicates

In your own analyses, you will have multiple conditions and (hopefully!) multiple replicates for those conditions. _Technical_ replicates are usually merged after FASTQC analysis to ensure that the sequencing quality is adequate. FastQ files can be concatenated at the read level or BAM files can be merged after alignment using SAMtools. 

_Biological_ replicates should be analyzed individually first and then compared at the peak call level. Key questions to ask are whether replicates correlate well and if there is substantial peak overlap. The current state-of-the-art for analyzing ChIP-Seq replicates and setting thresholds is the [Irreproducible Discovery Rate](https://sites.google.com/site/anshulkundaje/projects/idr) (IDR), which compares a pair of ranked lists of peaks and creates a curve to quantitatively determine the extent to which the ranks are no longer consistent across the replicates. The method was developed and used extensively for the ENCODE and modENCODE projects and is part of their [ChIP-seq guidelines](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3431496/). The method is not yet available in the standard Galaxy installation, however.

In the meantime, there are simple things in Galaxy that you can do to analyze replicates and additional samples, such as intersecting and subtracting peaks to get common and unique regions in two samples. 

### Bringing in replicates and another sample

Up to now we have been analyzing a single ChIP experiment (Nanog-Rep1-chr12 sample and Input-Rep1-chr12 control) to save time. Now we will bring three other ENCODE data sets into our analysis. We have generated the necessary files -- the second H1Hesc Nanog replicate and two replicates for H1Hesc Pou5f1 (Oct4)  -- for you and placed them in the Shared `Data Library` under `ChIP-Seq Data`; they can be found in the `Additional Sample Data` folder. Open up this folder and import the following peak calls for each of the other 3 ENCODE samples to your history (making sure to specify the bed format):

* `MACS_Nanog_Rep2.chr12.bed`
* `MACS_Pou5f1_Rep1.chr12.bed`
* `MACS_Pou5f1_Rep2.chr12.bed` 

To increase our confidence in the peak calls, we will combine our replicate files and take the intersection of the two. Click on `Operate on Genomic Intervals` and `Concatenate` the two Nanog replicates to combine them into one file. Next, use the `Cluster` tool on the concatenated data to combine overlapping peak calls using the default parameters. 

> How many peaks are retained? What fraction of the individual replicates are retained? 

A simple heuristic used by the ENCODE project prior to IDR was to retain replicates for analysis if either 80% of the top 40% of identified targets in one replicate were among the targets in the second replicate; or 75% of target lists were in common between both replicates.

Note that the resulting peak calls are dominated by the _“weakest”_ replicate. You will probably have noticed that there is also an `Intersect` tool and may be wondering why we did not use it directly on the two replicates. If we had, only peaks in the first replicate that overlap with the second would be returned, i.e. overlapping regions would not be merged to form a larger region encompassing the coverage from both replicates.

> Repeat these steps for the Pou5f1 replicates to prepare to look for differential enrichment of binding sites.

### Differential binding

To identify sites that have differential binding, across two conditions, developmental stages, factors, etc., we will use Galaxy’s `Subtract` tool on the intersected peak calls for Nanog and Pou5f1. Select the clustered Pou5f1 file for the first input and the clustered Nanog file for the second input, and return `intervals with no overlap`. The resulting dataset contains regions where Nanog binds but Pou5f1 does not. You can then switch the inputs to find regions where Pou5f1 binds but Nanog does not. 

Note: You can also use MACS directly to find differential binding between two conditions by treating one of the samples as the control. 

> Find regions where both TFs bind using the approach above for intersecting two replicates.

---
**Move on to [Motif detection and functional enrichment](http://scriptogr.am/ohofmann/post/chip-seq-enrichment-analysis).**
