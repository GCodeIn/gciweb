# gciweb
A poorly documented static site generator

## File structure
Each project is organized into a site directory. Each site directory has three
subdirectories, `assets`, `pages`, and `templates`.

These docs aren't great, so look at the files in `site` in this repo (a demo
site) if you get confused.

### `assets`
The `assets` directory will be placed at `/assets` on the Web site. For
example, if you have an image `my_cat.jpg` in `assets/images/my_cat.jpg`, you
would use `<img src=/assets/images/my_cat.jpg>` in an HTML file. You can
arrange the files in `assets` however you want.

### `pages`
The `pages` directory is the top-level page directory.

#### Page directories
In GCIWeb, all pages are contained in page directories. A page directory
contains a JSON configuration file, `data.json`; any .html files needed by the
template specified in `data.json`; and zero or more other page directories.

`data.json` is the configuration file for the page. It must, at least, have
the property `template`. This specifies the template name, not including the
path and `.html`. The rest of the properties will be substituted into any
occurrence of `{{{property name}}}` in the template.

The `.html` files will be substituted into any occurrence of `{{name of file
not including .html}}` in the template.

For each page directory in the source site, a directory with the same path
will be created under `built` (in the same directory as `pages`, `assets`, and
`templates`) containing `index.html`, which is the output of the build process
for that page.

### Templates
The `templates` directory contains one or more HTML files. Anywhere a property
from `data.json` should be substituted in (e.g. a page title), use 
`{{{property}}}`. Wherever a `.html` file from the page directory should be
substituted in (e.g. the main body of the page), use `{{file name not
including .html}}`.

## Installation
    sudo cp gciweb /usr/bin/gciweb

## Usage

    gciweb

for site in current directory, builds in `./built`

    gciweb <dir>

for site in other directory, builds in `dir/built`

## Demo site
To try out GCIWeb, run `./gciweb site` and check `./site/built`.

## GitHub Pages Deployer
It would be really nice to have a program that would watch for GitHub pushes
or commits, fetch the latest source, and deploy to GitHub Pages. If you want
to write this, please let us know in an issue or on our IRC channel, #gcodein
on Freenode!
