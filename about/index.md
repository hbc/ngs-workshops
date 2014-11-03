---
layout: page
title: About the site
tags: [about, introduction,hbc,support]
modified: 2014-08-08T20:53:07.573882-04:00
comments: false
image:
  feature: banner-dna-colour.jpg
  credit: Taraki / Fotolia
---

The sequencing workshops are run by the [Bioinformatics Core](https://hsphbio.ghost.io/) at the [Harvard School of Public Health](http://www.hsph.harvard.edu/), sponsored by the [Tools and Technology Program of Harvard Medical School](http://hms.harvard.edu/departments/tools-and-technology) and the [Harvard NeuroDiscovery Center](http://www.neurodiscovery.harvard.edu/).

Courses are being run as hands-on sessions with a focus on next-gen sequence data in public health and stem cell biology. We make use of the Galaxy framework to ensure little prior computational experience is required and to help establishing a few key concepts that are important to any computational research:

 * organizing your _in silico_ work just as well as any other lab work, 
 * focus on reproducibility of your results, and 
 * document your work and make it available to the scientific community. 

Those three skills alone will put you ahead of the majority of practicing bioinformaticians.

### The importance of reproducible science

If you haven't heard about the [Duke Clinical Trials](http://www.nytimes.com/2011/07/08/health/research/08genes.html?_r=2) and how simple index errors spiraled out of control, ultimately resulting in several clinical trials based on false data I _strongly_ recommend watching [Keith Baggerly's talk](http://videolectures.net/cancerbioinformatics2010_baggerly_irrh/). Promise it's worth the time.

While the data issues described by Keith were not accidental not all bad data is generated with malicious intent. As a [recent study](http://www.reuters.com/article/2012/03/28/us-science-cancer-idUSBRE82R12P20120328) noted the majority of biomedical studies can not be reproduced:

> "Of 47 cancer projects at Bayer during 2011, less than one-quarter could reproduce previously reported findings, despite the efforts of three or four scientists working full time for up to a year. Bayer dropped the projects."

And quite a few of these discrepancies arise due to a perceived need to come up with a likable scientific story:

> "We went through the paper line by line, figure by figure," said Begley. "I explained that we re-did their experiment 50 times and never got their result. He said they'd done it six times and got this result once, but put it in the paper because it made the best story. It's very disillusioning."

TEST

[Ionnidis et all](documents/introduction/Nat%20Genet%202009%20Ioannidis.pdf)[^1] (PDF) described similar findings in a survey of array data -- one of the best understood high-throughput data sources in bioinformatics -- published in Nature Genetics:

> "One table or figure from each article was independently evaluated by two teams of analysts. We reproduced two analyses in principle and six partially or with some discrepancies; ten could not be reproduced."
And the [Science Exchange Blog](http://blog.scienceexchange.com/2012/04/the-need-for-reproducibility-in-academic-research/) has additional examples if you are still curious.

### Keeping notes

To avoid creating similar problems for your peers keeping notes on your work is paramount. If you are interested in the topic we recommend working through articles from [Titus Brown's blog](http://ivory.idyll.org/blog/) and familiarizing yourself with automated systems such as [IPython](http://ipython.org/) (web-based notebooks for Python), [knitr](http://yihui.name/knitr/) (dynamic reports in R) or initiatives such as [Sage's Synapse](https://synapse.sagebase.org/) (data repositories and workflow documentation). 

In this course Galaxy, our analytical framework, will keep most of the notes for you. You will most likely still need to document additional work and keep track of files, papers and other documents. Whatever system you use for this is fine -- be it Evernote, GitHub, or a simple folder-based system recommend by [Bill Noble](/documents/introduction/PLoS%20Comput%20Biol%202009%20Noble.pdf)[^2] (PDF)

### Dissemination

While keeping good notes is one thing, making them available along with primary and derived data is just as important, Frustrated by [closed lab protocols](http://ivory.idyll.org/blog/a-call-for-open-lab-protocols.html) Titus Brown and [Brad Chapman](http://bcbio.wordpress.com/) have suggested a [simple checklist](http://ivory.idyll.org/blog/blog-review-criteria-for-bioinfo.html) for publications in bioinformatics, and Titus himself [leads the way](http://ivory.idyll.org/blog/replication-i.html) with a recent manuscript, making just about everything available:

* a link to the paper itself, in preprint form, stored at the arXiv site;
* a tutorial for running the software on a Linux machine hosted in the Amazon cloud;
* a git repository for the software itself (hosted on github);
* a git repository for the LaTeX paper and analysis scripts (also hosted on github), including an ipython notebook for generating the figures (more about that in my next blog post);
* instructions on how to start up an EC2 cloud instance, install the software and paper pipeline, and build most of the analyses and all of the figures from scratch;
* the data necessary to run the pipeline;
* some of the output data discussed in the paper.

For this course almost all work we will be doing is captured automatically and can be shared with others through a simple URL, but as you start utilizing tools outside of Galaxy (or similar systems such as [GenePattern](http://genepattern.broadinstitute.org)) we strongly recommend to browse through some of these materials.

## Contact information

If you have any questions about the course materials do not hesitate to ask [Radhika Khetani](mailto:khetani.r@gmail.com) or  [Oliver Hofmann](mailto:ohofmann@hsph.harvard.edu) directly. You can also get hold of Oliver on [Twitter](https://twitter.com/fiamh) or _in emergencies_ give him a call at +1 617 365 0984. 


[^1]: Ioannidis, John P A, David B Allison, Catherine A Ball, Issa Coulibaly, Xiangqin Cui, Aedín C Culhane, Mario Falchi, et al. “Repeatability of Published Microarray Gene Expression Analyses.” Nature Genetics 41, no. 2 (February 1, 2009): 149–155.
[^2]: Noble, William Stafford. “A Quick Guide to Organizing Computational Biology Projects.” PLoS Computational Biology 5, no. 7 (June 30, 2009): e1000424.


