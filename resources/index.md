---
layout: page
title: Resources
author: oho
tags: [about, introduction,hbc,support]
modified: 2014-08-08T20:53:07.573882-04:00
comments: false
image:
  feature: banner-tools.jpg
  credit: OZinOH
  creditlink: "https://www.flickr.com/photos/75905404@N00/7126146307/in/photolist-bRHn2v-5ZEy3v-njeKMd-34Ydj3-6jWS5p-bRHngB-69kvVh-81qMNV-jfdpir-3coNmc-e3oR2D-6aQB7U-ebk9uv-5X2NpW-9KQoQd-2DWGDT-hQQFyG-fkmB7T-pEf1ab-8EatV2-8DiwUK-M1h2U-66WjNR-eHQ3T6-mhpdd-7Vy7hY-3r7wnw-oUmJH-fdyRbJ-fZijk2-gm5988-8iy9Dy-63FsG8-4Qj8Tm-dM3o9g-agpmaQ-4WpAb-7SP4bh-ta4a-63FsXn-9NcgEi-cnHKtu-CTVZj-iMqGkR-8Br5FX-6VHf97-apdrrN-9rPDkF-8x4RCw-4rJRhJ/"

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

## Galaxy

The workshop sessions rely on [Galaxy](http://usegalaxy.org), an open-source framework for biomedical data analysis developed by the Galaxy Team at Penn State. We will work you through a few basic workflows, but the Galaxy wiki has dozens of additional [tutorials and screencasts](http://wiki.g2.bx.psu.edu/Learn/Screencasts) that are worth exploring.


### Galaxy installation for the course

During the courses and workshops we will be using a CloudMan installation of Galaxy running in Amazon's AWS environment. You can reach the Galaxy instance at [http://23.23.134.25/](http://23.23.134.25/). 

Remember to register an account during your first visit as this will enable personal histories, sharing of data and much more.
{: .notice}

### Public galaxy installations

After the course you can pick from an extensive list of [public Galaxy instances](http://wiki.g2.bx.psu.edu/Public%20Galaxy%20Servers). Note that most public servers have strict limits on how much data you can store (a quota) which can be somewhat limiting when it comes to NGS analysis.

### Deploying your own Galaxy instance

While you can analyze smaller data sets on any of the public Galaxy instances most NGS projects tend to run into quota problems sooner rather than later. For that reason it might make sense to set up your own Galaxy instance. We have summarized the different options to [set up your own Galaxy instance](TBA), but do not hesitate to contact us with questions.


### Galaxy training material

Other than the already mentioned screencasts and tutorials on the [main Galaxy site](http://wiki.g2.bx.psu.edu/Learn/Screencasts) a host of other groups are using Galaxy for training purposes. A few notable highlights include:

* A turnkey tutorial from the Galaxy team, held at [ISMB 2010](https://main.g2.bx.psu.edu/u/aun1/p/ismb2010-demo)
* The UC Davis training courses tend to have great [introductions to Galaxy](http://training.bioinformatics.ucdavis.edu/docs/2012/05/RNA/galaxy-intro.html) if you want to get some additional experience
* ICB at Cornell University made their [Galaxy workshop materials](http://chagall.med.cornell.edu/galaxy/) available


## … and beyond

As useful as Galaxy can be, at some point you will want to branch out to using the command line and creating some basic scripts to make your life easier. Take a look at the Unix-sections of [the Perl and Unix Primer for Biologists](http://korflab.ucdavis.edu/unix_and_Perl/) which should familiarize yourself with the shell and basic file manipulation skills. Once you are comfortable navigating around your folders try to run some of the tools you used in Galaxy on the command line -- the [FASTQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/) analysis might be a good starting point.

From there, take a look at some of the swiss army knives of NGS analysis:

* The [FastX Toolkit](http://hannonlab.cshl.edu/fastx_toolkit/ ) to manipulate reads* [BioPieces](http://code.google.com/p/biopieces/) with dozens of little helpers
* [BEDTools](http://code.google.com/p/bedtools/) to slice and dice BED, BAM or VCF files (merge, intersect, sort, etc.)

This maturity in tool development is driven by a rapid convergence towards a small list of minimal standards in order to allow a more modular design of workflows as well as to facilitate data exchange between components, most of which you have encountered during the last sessions:

* [FASTQ](http://maq.sourceforge.net/fastq.shtml), Sequence and quality information
* [SAM/BAM](http://samtools.sourceforge.net/), Alignments
* [VCF](http://vcftools.sourceforge.net/specs.html), Variants

These standards and other existing software frameworks facilitate the development of sequence analysis environments such as the Broad’s [Genome Analysis Toolkit](http://www.broadinstitute.org/gsa/wiki/index.php/The_Genome_Analysis_Toolkit), eventually allowing you to mix and match your workflows as needed. 

Finally, [Software Carpentry](http://software-carpentry.org/): one of the best resources on the web to get you started with programming. Whether you use Python, Ruby, Perl or some other programming language to explore your first basic scripts, do set aside a weekend to work the Carpentry's materials. While the best practices listed might seem overwhelming in the beginning they are kept fairly simple and will be absolutely invaluable down the road.

### NGS resources

You cannot go wrong by simply following the workflows outlined by large-scale genomic papers coming from any of the big sequencing centers, although this frequently requires delving through the supplementary material and online information. For standard tasks the [Galaxy tutorial workflows](http://wiki.g2.bx.psu.edu/Learn/Screencasts) and the [SeqAnswers best practices](http://seqanswers.com/wiki/How-to) are also a great starting point. Beyond these starting points, one of the best resources for NGS questions is the [SeqAnswers forum](http://seqanswers.com/forums/forumdisplay.php?f=18) and [Wiki](http://seqanswers.com/wiki/SEQanswers). Take the time to read through the available information and make use of the search function. The [BioStar](http://www.biostars.org/) website can also be worth exploring, but has a lower signal/noise ratio.

## Remaining current

Staying up-to-date is an ongoing challenge in research. Rather than provide a list of papers and reviews that will likely be outdated within months I strongly recommend following [Stephen Turner's approach](http://gettinggeneticsdone.blogspot.com/2012/05/how-to-stay-current-in.html) which is almost completely identical to mine. Identify blogs, twitter accounts and websites that are relevant, subscribe to their [RSS feeds](http://en.wikipedia.org/wiki/Web_feed) and spend twenty minutes each day sifting through them. 

## Additional training material and workshops

The [MSU summer course](http://bioinformatics.msu.edu/ngs-summer-course-2012) is terrific and in addition makes all material available for those who could not attend. Also, most of the material of [Birt's NGS course](http://informaticstraining.hms.harvard.edu) are accessible. Other centers are making their training material available; among these the course material from the [UC Davis Bioinformatics Core](http://training.bioinformatics.ucdavis.edu/documentation/) really stand out.

