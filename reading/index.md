---
layout: page
title: Reading
tags: [papers,publications,ngs,background]
modified: 2014-08-08T20:53:07.573882-04:00
comments: false
image:
  feature: banner-papers.jpg
  credit: GalleryHip
  creditlink: http://galleryhip.com/pile-of-papers-on-desk.html
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

This page contains pointers to additional reading material and external resources relevant to the course. The page will be updated prior to every workshop and links and tips are very much welcome!

## General considerations

* Things to consider [when picking a sequencing facility](http://biomickwatson.wordpress.com/2013/01/21/ten-things-to-consider-when-choosing-an-ngs-supplier/)
* Excellent list of [introductory NGS papers](http://core-genomics.blogspot.com/2012/12/introductory-references-for-ngs-newbies.html?spref=tw)
* A more detailed list focusing on [all things RNA-Seq](http://www.ngswatch.com/rna-seq/) or [DNA-Seq](http://www.ngswatch.com/dna-seq-101/)
* Search portal for [NGS papers linked to disease, platform, mutations and Co](http://bioinfo.mc.vanderbilt.edu/NGS/index.html)

## Introduction

* [Organizing your data](..../documents/introduction/PLoS%20Comput%20Biol%202009%20Noble.pdf) (PDF)
* [Array reproducibilty](../documents/introduction/Nat%20Genet%202009%20Ioannidis.pdf) (PDF)
* [Keith Baggerly video lecture](http://videolectures.net/cancerbioinformatics2010_baggerly_irrh/)
* [James Hadfield on better NGS experiments](http://core-genomics.blogspot.com/2012/10/how-to-do-better-ngs-experiments.html)

## QC and general sequence alignment

* [FASTQ format](../documents/QC/Nucleic%20Acids%20Res%202009%20Cock.pdf) (PDF)
* [k-mer analysis](../documents/QC/PLoS%20ONE%202010%20Schr%C3%B6der.pdf) (PDF)
* [ContEst](../documents/QC/Bioinformatics%202011%20Cibulskis.pdf) (PDF)
* [SeqTrim](../documents/QC/BMC%20Bioinformatics%202010%20Falgueras.pdf) (PDF)

If you are curious to learn more about how nucleotides in FASTQ files are determined and associated with a quality score, this review by [Christian Ledergerber and Christophe Dessimoz](../documents/QC/Briefings%20in%20Bioinformatics%202011%20Ledergerber.pdf) (PDF)  provides a thorough summary. If you are more interested in 'fixing' false calls, take a look at [Reptile](../documents/QC/Bioinformatics%202010%20Yang-1.pdf) (PDF) (or browse through this [recent review](../documents/QC/Brief%20Bioinformatics%202012%20Yang.pdf) (PDF) for a more general summary), one of the many available NGS error correction algorithms. Finally, the meeting notes from a [Bioinfo Core call on NGS QA](http://bioinfo-core.org/index.php/9th_Discussion-28_October_2010) might provide insight into typical failure modes of sequencing experiments, 

* [Comparison of aligners](../documents/Exome%20Seq/J%20Hum%20Genet%202011%20Bao.pdf) (PDF)
* [Live summary of HTS Mappers](http://wwwdev.ebi.ac.uk/fg/hts_mappers/) at the EBI
* [SAM format](../documents/Exome%20Seq/Bioinformatics%202009%20Li-3.pdf) (PDF)

## RNA-seq alignment

* [RNA-seq with R](http://bioinf.wehi.edu.au/bioinfosummer2010/materials/RNAseq_Mapping_Tutorial.pdf) (PDF)
* [SeqAnswer's HowTo](http://en.wikibooks.org/wiki/Next_Generation_Sequencing_(NGS)/RNA)
* [UC Davis Course](http://training.bioinformatics.ucdavis.edu/docs/2012/05/RNA/index.html)
* Gunnar Raetsch's [240 slide tutorial on NGS sequencing](http://raetschlab.org:10080/fml-migrated/raetsch/lectures/ismb10tutorial) has a lot of information about RNA-seq biases
* [TopHat manual](http://ccb.jhu.edu/software/tophat/index.shtml)
* [Cufflinks manual section](http://cufflinks.cbcb.umd.edu/manual.html#cufflinks)
* [Trinity](http://trinityrnaseq.sourceforge.net/) (_de novo_ assembly)

## RNA-seq quantification

* [Required read depth](../documents/RNA-seq/Genome%20Res%202011%20Toung.pdf) (PDF)
* [RNASeqQC](http://www.broadinstitute.org/cancer/cga/rna-seqc)
* [RNA-seq biases](../documents/RNA-seq/ANALYTICAL%20BIOCHEMISTRY%202011%20Sendler.pdf) and [coverage variance](../documents/RNA-seq/1471-2105-13-S6-S4.pdf) (PDF)
* [DESeq](http://bioconductor.org/packages/release/bioc/html/DESeq.html), [DEXSeq](http://bioconductor.org/packages/release/bioc/html/DEXSeq.html)

## Exome-seq evaluation

* [Landmark exome-seq paper](../documents/Exome%20Seq/Nature%202009%20Ng.pdf) (PDF)
* [Minimal exome-seq example](../documents/Exome%20Seq/N%20Engl%20J%20Med%202010%20Musunuru.pdf) (PDF)
* Genome Biology's [special issue on exome-seq](http://genomebiology.com/content/12/9)  (PDF)
* SeqAnswer's [How-to for exome-seq](http://seqanswers.com/wiki/How-to/exome_analysis)

## Variant calling and visualization

* The [Genome Analysis Toolkit](http://www.broadinstitute.org/gsa/wiki/index.php/Main_Page) and [paper](../documents/Variant%20Discovery/Genome%20Res%202010%20McKenna.pdf) (PDF)
* Overview of [genotype and SNP calling approaches](../documents/Exome%20Seq/Nat%20Rev%20Genet%202011%20Nielsen.pdf) (PDF)
* [VCF specifications](http://www.1000genomes.org/node/101) and [paper](../documents/Variant%20Discovery/Genome%20Biol%202010%20Reese.pdf) (PDF)
* Typical [sequencing workflow](../documents/Variant%20Discovery/Nat%20Genet%202011%20Depristo.pdf) (PDF) from DePisto et al, including multiple experimental designs
* [VarScan 2](http://massgenomics.org/2010/02/varscan-2-released-on-sourceforge.html), one of the many variant calling tools; this one specializes in calling variants utilizing matched tumor/normal samples
* [Slider II](../documents/Variant%20Discovery/Bioinformatics%202010%20Malhis.pdf) (PDF) as an alternative variant caller in shallow coverage situations
* [SomaticSniper](http://gmt.genome.wustl.edu/somatic-sniper/current/) with a focus on cancer/normal comparisons


## VCF annotation, filtering and functional assessment

* [Lancet paper](../documents/Function/The%20Lancet%202010%20Ashley.pdf) (PDF) on trying to find actionable clinical information from WGS
* [dbSNP](http://www.ncbi.nlm.nih.gov/projects/SNP/)
* [HapMap](http://hapmap.ncbi.nlm.nih.gov/)
* [snpEff](http://snpeff.sourceforge.net/)
* [Variant Effect Predictor](http://www.ensembl.org/info/docs/tools/vep/index.html) 
* [VAT](http://vat.gersteinlab.org/index.php) ([Sample report](http://vat.gersteinlab.org/summary.php?dataSet=vat.222&setId=222&annotationSet=gencode7&type=coding))
* [Grail](http://www.broadinstitute.org/mpg/grail/grail.php) ([manuscript](../documents/Function/PLoS%20Genet%202009%20Raychaudhuri.pdf),  (PDF))
* [Dapple](http://www.broadinstitute.org/mpg/dapple/dapple.php) ([manuscript](../documents/Function/PLoS%20Genet%202011%20Rossin.pdf), (PDF))
* [MuSiC](http://massgenomics.org/2012/07/mutation-significance-in-cancer.html)

Coverage of genomic testing has been increasing in the popular press. Matthew Herper's article in Forbes [the promise and chaos of cancer medicine](http://blogs.forbes.com/matthewherper/2011/06/05/cancers-new-era-of-promise-and-chaos/), as are recent individual case descriptions published in the NYT ([here](http://www.nytimes.com/2012/07/08/health/in-gene-sequencing-treatment-for-leukemia-glimpses-of-the-future.html?pagewanted=all), [here](http://www.nytimes.com/2012/07/09/health/new-frontiers-of-cancer-treatment-bring-breathtaking-swings.html?ref=science&pagewanted=all) and [here](http://www.nytimes.com/2012/07/10/health/genetic-test-changes-game-in-cancer-prognosis.html?pagewanted=1&pagewanted=all)). More and more people are also starting to look into rare diseases [on their own](http://blog.ted.com/2012/07/17/newly-discovered-gene-may-explain-4-year-olds-rare-disease-thanks-to-ted-fellow-jimmy-lin/) or with the help of [crowd-sourcing](http://cmtproject.blogspot.com/2012/05/new-developments.html). 

If you are interested in learning about new studies and workflows to get identify causal mutations, make sure to follow Dan Koboldt at [MassGenomics](http://massgenomics.org).

## ChIP-Seq

* [GREAT](../documents/ChIP-Seq/Nat.%20Biotechnol.%202010%20McLean.pdf) (PDF) for functional interpretation of peaks
* [DREME](../documents/ChIP-Seq/Bioinformatics%202011%20Bailey.pdf) (PDF) for motif discovery
* [Peak Correlation](../documents/ChIP-Seq/Bioinformatics%202012%20Chikina.pdf) (PDF) to evaluate ChIP-eq data similarity
* [Irreproducible Discovery Rate](https://sites.google.com/site/anshulkundaje/projects/idr) to understand replicate information
* [Cistrome](http://cistrome.org/Cistrome/Cistrome_Project.html), Shirley Liu's set of ChIP-seq workflows and tools
* [Nebular](http://nebula.curie.fr/), another Galaxy-based ChIP-Seq framework
