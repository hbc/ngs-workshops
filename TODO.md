## Changes to the course notes

* Strongly suggest to include a link and/or discussion of the [Leek group guide to Genomics Papers](https://github.com/jtleek/genomicspapers/). Awesome resource and one I point most new students at.
* The [mother of all NGS papers resource](http://www2.informatik.hu-berlin.de/~hakenber/links/nextgen.html) is worth adding to the resource section and maybe should be pointed out during the courses. 
* Would love to work a [code of conduct](http://angus.readthedocs.org/en/2014/code-of-conduct.html) into our workshop materials ("tl; dr: Don’t be a jerk.")


## Generic course materials

Workshops and courses that could be useful as references:

* All things [Software Carpentry](http://swcarpentry.github.io/bc/)
* Ark Genomics (nowadays Edinburgh Genomics) held an [introduction to NGS workshop](http://www.ark-genomics.org/events-online-training/eu-training-course) with an emphasis on the command line, AWS and Co. Mick Watson might have newer versions. 
* This [UiO course](https://wiki.uio.no/projects/clsi/index.php/INF-BIOX121_H14) runs the whole gamut from variant calling to ChIP-Seq to miRNA/mRNA, statistics and command line. Might be worthwhile to compare and contrast. 
* Wide range of tutorials from the [Australian team](https://genome.edu.au/wiki/Learn), again useful for comparison. They have inquired whether we are interested in sharing course materials and Co. Contact is Andrew Lonie.
* The [EBI's Train Online](http://www.ebi.ac.uk/training/online/) section is worth linking to.
* Still didn't have a chance to work through [Titus' 2013 workshop](http://ged.msu.edu/angus/tutorials-2013/).
* The [Brabaham workshops](http://www.bioinformatics.babraham.ac.uk/training.html) might be worth skimming through, too.
* The [UC Davis workshops](http://training.bioinformatics.ucdavis.edu/documentation/). Period. 
* Materials and handouts (in PDF/LaTeX, no less) from a [2-day workshop on NGS](https://github.com/nathanhaigh/ngs_workshop).


## Introduction to Galaxy

The Galaxy Intro seems to be working well, but I still like the original version that used DNAse hypersensitive sites, and [MassGenomics has a great article on these](http://massgenomics.org/2012/09/encode-regulatory-variation-in-the-human-genome.html).


## Unix and Programming

* Work through the [Software Carpentry Repo](https://github.com/swcarpentry/bc).
* For R the online [Fiddle](http://www.r-fiddle.org/#/) environment might work rather than a full RStudio installation.
* An [online training environment](http://swirlstats.com/) for R.
* Had good experience with the Unix section of the [Unix & Perl Primer](http://korflab.ucdavis.edu/unix_and_Perl/).
* For Python the [Python for Biologist](http://pythonforbiologists.com/index.php/introduction-to-python-for-biologists/) course might be useful.
* The [Try Github](https://try.github.io/levels/1/challenges/1) environment along with the [git simple guide](http://rogerdudler.github.io/git-guide/) to get people started.


## Genome assembly

Not sure there is demand for genome assembly, but this could be combined with RNA-Seq _de novo_ methods:

* Lex put his [assembly course materials](https://github.com/lexnederbragt/INF-BIOx121_fall2014_de_novo_assembly) on GitHub.
* An [assembly exercise](https://flxlexblog.wordpress.com/2014/11/04/on-the-benefits-of-open-for-teaching/) (and a good note on open teaching).
* Great way to merge an IPython class with an [assembly tutorial](http://nbviewer.ipython.org/url/files.figshare.com/1075540/P3D7_CLEAR_NOTE.ipynb), via Jason Chin.
* A somewhat [older bacterial genomics course](http://nickloman.github.io/notebook%20teaching/2012/12/04/bacterial-genomics-course/) from Nick, still worth sifting through. 
* In case we ever need to teach PacBio and Co: the [PacBio Training Wiki](https://github.com/PacificBiosciences/Bioinformatics-Training/wiki).
* Nice summary of [assembly metrics](http://keithbradnam.com/blog/2013/7/8/why-is-n50-used-as-an-assembly-metric.html?utm_content=buffer8420f&utm_source=buffer&utm_medium=appdotnet&utm_campaign=Buffer).


## RNA-Seq

Worth going over the course materials with Rory and Lorena. Would love to add some more modern methods to the course (e.g., STAR, eXpress, others):

* See if anything can be adapted from the recent [UC Davis Galaxy courses](http://training.bioinformatics.ucdavis.edu/docs/2014/12/december-2014-workshop/).
* Would strongly suggest linking to the [RNA-Seq 1010 paper list](http://www.ngswatch.com/rna-seq/) or incorporating it into our own reading materials.
* Stephen posted his materials from a recent [RNA-Seq course](http://gettinggeneticsdone.blogspot.com/2014/11/rna-seq-data-analysis-course-materials.html).



## Variant calling

The oldest course; this certainly needs some work. In particular I'd suggest introducing [joint calling methods](http://bcb.io/2014/10/07/joint-calling/) and look into the following links:

* NGSWatch has a nice [list of relevant articles](http://www.ngswatch.com/dna-seq-101/) with an emphasis on NGS technologies, approaches, etc.
* Blend [ExAc](http://macarthurlab.org/2014/11/18/a-guide-to-the-exome-aggregation-consortium-exac-data-set/) into variant calling.
* The [SeqAnswers guide](http://seqanswers.com/wiki/How-to/exome_analysis) might have some ideas for a command-line based version.
* Erik has a [mini-tutorial on FreeBayes](http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html)
* If you are really adventurous.. NGS [on a Raspberry Pi](http://www.walesgenepark.cardiff.ac.uk/wp-content/uploads/2013/04/1.1-Introductory-NGS.pdf).


## ChIP-Seq

Mostly a list of reading materials. Might be worth to explore what docs are available by now for [Cistrome](http://www.cistrome.org/Cistrome/Cistrome_Project.html) and [Cistemaic](http://woldlab.caltech.edu/wiki/Cistematic).

* UC Berkeley, http://www.stat.berkeley.edu/share/biolab/Courses/CIPF10/Data/Lecture3.pdf
* Max-Planck, http://lectures.molgen.mpg.de/Functional_Genomics_WS1112/ChIP-seq1.pdf
* German Cancer Research Center, http://gepard.bioinformatik.uni-saarland.de/teaching/ws-2011-12/special-topic-lecture-bioinformatics-next/lectures/ChlpSeq-NGS.pdf



### Chip-Seq reviews

* [Chip-Seq guidelines and practices of ENCODE/modENCODE](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3431496/)
* [Evaluation of Algorithm Performance in ChIP-Seq Peak Detectio](http://www.plosone.org/article/info:doi/10.1371/journal.pone.0011471)
* [Computation for ChIP-seq and RNA-seq studies](http://www.nature.com.ezp-prod1.hul.harvard.edu/nmeth/journal/v6/n11s/full/nmeth.1371.html)
* [ChIP-seq: technical considerations for obtaining high quality data](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3541830/)
* [Systematic evaluation of factor influencing ChIP-seq fidelity](http://lieblab.bio.unc.edu/publications/2012_05_ChIP-seq_fidelity.pdf)
* [Processing and analyzing ChIP-seq data: from short read to regulatory interactions](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3080774/pdf/elq022.pdf)


### Quality assessment and dealing with replicates

* [Phantompeakqualtools](https://code.google.com/p/phantompeakqualtools/)
* [IDR](https://sites.google.com/site/anshulkundaje/projects/idr)
* [ENCODE blacklist](http://hgwdev.cse.ucsc.edu/cgi-bin/hgFileUi?db=hg19&g=wgEncodeMapability)

### Peak calling

* [SPP](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2597701/)
* [MACS](https://dl.dropboxusercontent.com/u/76426/ChIP-seq/nprot.2012.101.pdf)
* [SICER](http://bioinformatics.oxfordjournals.org/content/25/15/1952.full)
* [Differential histone modification sites](http://www.ncbi.nlm.nih.gov/pubmed/22130888)
* [Encode Data](http://davetang.org/muse/2014/03/23/encode-rna-polymerase-ii-chip-seq/)
