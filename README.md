# Introduction to Next Generation Sequencing in Galaxy

Course materials (and website through GitHub Pages) from the [HSPH Bioinformatics Core](https://hsphbio.ghost.io/) using the [Minimal Mistakes](http://mmistakes.github.io/minimal-mistakes/theme-setup/) template system. Requires Jekull 2.x, see the [setup guide](http://mmistakes.github.io/minimal-mistakes/theme-setup/) for more information.

# Organization

Course materials are in `_posts` as "posts", static "pages" have their own directories along with an index file (e.g., `about/index.md`). Recommend pre-viewing any changes to the Markdown files with a local viewer such as [Marked 2](http://marked2app.com/).

To serve the website locally use Jekyll with a separate config file with just the `url` parameter changes:

> `url:              http://localhost:4000`

Then use `jekyll serve -w --baseurl "" --config _dev_config.yml `
