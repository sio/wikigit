# Project status

An idea. No implementation exists yet, not even a draft.


# Description

A static site generator for a simple wiki. Supports article versioning and
diffs based on git history. All texts should be written in Markdown (or
reStructured Text).

# Intended use case

A small group of authors writes documentation intended for a larger audience of
readers.

Authors are assumed to be tech-savvy enough to write texts with plain text
editor and manually apply markup (Markdown, reST, etc). Authors are to push the
texts into a Git repository with proper commit messages.

Website administrator generates a static set of HTML pages based on the
contents of Git repo (or a subdirectory of a Git repo) and publishes these
pages on the network (with any HTTP server or simply in a shared folder).

No assumptions about readers skill set are made. They are to access the
published documentation with any modern web browser. Readers are assumed to be
interested to see the changes between page versions, so there must exist a way
to show diffs in the web browser.


# Features and implementation ideas

Because (as far as I know) no such software exists, this has to be written from
scratch. Implementing yet another static site generator is an overkill for the
task, so I'm looking into extending the functionality of existing ones. I'm
most comfortable programming in Python, that's why this will probably be a
plugin for [Pelican][1].

The following features are currently considered:

### Page history with diffs

This is a raison d'être of this project. All pages should have the list of
previous versions with small descriptions of what has been changed (commit
messages). Every *older version* should be accessible, plus a *diff to current
version* and a *diff to previous* one. Generating other diffs between all
possible combinations of page versions is considered excessive and will not be
implemented.

This will be the core functionality of new Pelican plugin.

##### File hierarchy for generated HTML pages

Existing Pelican output:
```
output/path/to/article.html
or
output/path/to/article/index.html
```

Extra output enabled by this plugin:
```
output/path/to/article/
                       history/index.html
                       diff/commit1-to-current/index.html
                       diff/commit1-to-previous/index.html
                       diff/commit2-to-current/index.html
                       diff/commit2-to-previous/index.html
                       ...
```

All generated URLs are meant to be "clean" (ending in directory name with a
trailing slash). Alternative behavior might be enabled via configuration
variable but this is planned as a low priority task.

### Recent changes

Generating a site-wide list of recent changes seems useful. The list in
question should contain a sensible number of recent commits with links to
proper diffs. The number should be defined by a plugin variable and be
configurable via the `pelicanconf.py`.

This will be the extra functionality of new Pelican plugin.

### Orphaned pages

There should exist a way to list pages which cannot be accessed by a sequence
of hyperlinks from the main page.

This is the task for website administrator, not for authors or users. This will
not be included in the Pelican plugin. Another tool should be found for this
purpose, such tool almost certainly exists already. Its usage should be
included in the project documentation.

### Namespaces

Namespaces are a popular way to divide the wiki into segments by subject,
intended audience, etc. Pelican already offers tags and categories for this
purpose. No extra functionality is required.

### Wiki index, TOC for pages

Although this is not planned as a part of plugin functionality, generating page
index and tables of contents for individual pages is an important wiki feature.
I'm sure there are plugins for Pelican for this purpose, they just need to be
found and documented.

### Internal links

Connecting pages via internal hyperlinks is supported in all wiki engines.
Pelican offers {filename} shortcuts for internal links. That's enough for a
start. May be there exists a plugin which adds support for proper wiki-style
links.

### PDF export

Exporting pages to PDF makes sharing and printing of the documentation much
easier. I'll need to look into possible options for pre-generating PDF versions
of each article (only the latest version, no history or diffs here).

This functionality will not be included in the plugin.

### Search

Static sites do not offer *"real"* search, and this wiki implementation will
not be different. Wiki index plus external search tools (like Google) will have
to be enough.


# Contributing

This project is in the earliest stage of development, so it's difficult to
imagine it will attract any contributors. If you like my idea and are willing
to help, please contact me. I promise to behave responsibly and to treat all
contributors with respect.


# License and copyright
Copyright © 2017 Vitaly Potyarkin
```
    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.
```


[1]: https://github.com/getpelican/pelican
