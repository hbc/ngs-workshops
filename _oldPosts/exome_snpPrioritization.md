---
Date: 2013-01-16 14:30
Title: Exome-seq: SNP prioritization
Tags: ngs, vcf, annotation
Author: Oliver Hofmann
Contact: ohofmann@hsph.harvard.edu
Type: post
---

A vast number of algorithms exists to quantify the likely impact of a genetic variant. We will explore just a few options to generate additional information for single SNPs and provide pointers to approaches that try to identify functional enrichment from multiple samples and patient.

## Predicting SNP effects and prioritization

To simplify the analysis we will be using an aggregator, i.e., a tool that combines multiple annotation services, which accepts VCF-formatted data as input. Upload your annotated VCF file to [VAT](http://vat.gersteinlab.org/index.php) and explore the report. In the output, check for deleterious/damaging non-synonymous mutations or loss-of-function mutations. Pick one mutation and review it in IGV -- what is its coverage? 

> What kind of change is the variant causing?

VAT can also handle output from multiple samples (variant files), see the [VAT report for lanes 7/8 aligned with Bowtie](http://vat.gersteinlab.org/summary.php?dataSet=vat.222&setId=222&annotationSet=gencode7&type=coding) online.

If you are analyzing multiple samples command line based tools can be useful. One of the standard frameworks for this is [snpEff](http://snpeff.sourceforge.net/); a sample output file for lanes 7 and lane 8 is [available online](http://dynamic.gersteinlab.org/people/lh372/vat_cgi?mode=process&dataSet=vat.27560&annotationSet=gencode7&type=coding).

### Is this useful?

Functional annotation of human genome variation is [a hard problem](http://massgenomics.org/2012/06/interpretation-of-human-genomes.html), but results from the last few years have been quite impressive. Dan Koboldt at WashU went through the 2011 literature and collected a large list of [disease-causing gene discoveries in disorders](http://massgenomics.org/2011/12/disease-causing-mutations-discovered-by-ngs-in-2011.html) and [cancer](http://massgenomics.org/2012/01/cancer-genome-and-exome-sequencing-in-2011.html), frequently with [relevance to the clinic](http://massgenomics.org/2010/04/why-we-sequence-cancer-genomes.html). A current manuscript studying Cystic Fibrosis shows that in some cases even [moderate samples sizes](http://www.ncbi.nlm.nih.gov/pubmed/22772370?dopt=Abstract) can be useful. Results are all but guaranteed, though -- for example, here are just the [most likely reasons why you cannot find a causative mutation in your data](http://massgenomics.org/2012/07/6-causes-of-elusive-mendelian-disease-genes.html).

In addition, sequencing errors and systematic changes to sample materials as part of the DNA extractation and library preparation process are a serious problem. Nick Lohman has a good summary of just [some of the known error sources](http://pathogenomics.bham.ac.uk/blog/2013/01/sequencing-data-i-want-the-truth-you-cant-handle-the-truth/) in a recent blog post triggered by a publication from the Broad Institute on [artifactual mutations due to oxidative damage](http://nar.oxfordjournals.org/content/early/2013/01/08/nar.gks1443.full.pdf?keytype=ref&ijkey=suYBLqdsrc7kH7G) -- in this case even analysis of the sample data with different sequencing technologies and bioinformatic workflows would not have made a difference. 


## Functional enrichment

Additional tools can be used to re-prioritize SNPs when trying to make sense of data from a larger cohort. Most have been developed to gain additional information from GWA results by exploring variants beyond those reaching genome wide significance, but many can be adapted to combine candidate regions or genes from other data sources where the problem of finding relevant variants is compounded by inter-patient differences; i.e., the problem shifts from finding functional variants in single patients to finding consistency in a patient cohort, particularly for complex diseases.

A framework developed for GWAS data is [DAPPLE](http://www.broadinstitute.org/mpg/dapple/dapple.php) which connects variants to gene regions in LD before trying to find interacting genes and gene products to prioritize SNPs for validation. As a test, submit some [sample regions](https://dl.dropbox.com/u/407047/Blog/Prioritization/sampleRegions.txt) to the system.

Make sure to state that this is a `test run` with only 50 iterations, ask for a `plot` to be returned, and set `nearest gene` to false. We assume no prior knowledge and ask for links between all genes rather than just connections between query genes to seed genes. Once the system mails you your results take a look at the generated PDF and the prioritized genes. 
> What functional enrichment is detected in the generated network? What disease are you most likely dealing with?

Other systems such as [Grail](http://www.broadinstitute.org/mpg/grail/grail.php) use text mining approaches, that is, information obtained from analyzing PubMed abstracts, to link candidate genes based on co-occurring keywords. 

> Submit another [sample SNPs set](https://dl.dropbox.com/u/407047/Blog/Prioritization/sampleSNPs.txt) to the Grail server and select parameters as follows: `hg18`, `CEU population`, `Pubmed 2011`, `gene size correction is requested`, `query all genes`, `seed genes equal query genes`. Look at the report (this may take up to an hour) -- what disease are those variants most likely associated with?

Whether you used GRAIL or DAPPLE, extract the [the top genes](https://dl.dropbox.com/u/407047/Blog/Prioritization/dappleTopHits.txt) from the results (or use the link) and submit them to the [GeneMania](http://www.genemania.org/) system using default parameters to gain some additional insight.

Other systems can make use of case/control information, or sift through matched tumor/normal samples; [MuSiC](http://massgenomics.org/2012/07/mutation-significance-in-cancer.html), a recent release to analyze cancer mutation data sets also tests for pathway enrichment, known mutations and mutual exclusive mutations before linking findings to clinical covariates.

