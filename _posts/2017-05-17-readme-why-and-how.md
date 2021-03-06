---
layout: post
title: "README.md: Why? and How?"
feature-img: assets/img/pexels/desk-coffee.jpg
tags: [README]
author-id: nettle
excerpt_separator: <!--more-->
---

# Why?

For those who work with [FOSS](https://wikipedia.org/wiki/FOSS) (Free and Open Source Software)
there is no such a question - `Why README.md?`<br>
The Source Code is open and published, products are free and can be used by anyone,
so README file is what user read first to get know the product and/or the code.
The README is an "entry point" for the FOSS projects.
<!--more-->
Especially if they are hosted at [GitHub](https://github.com) or similar Open Source portals
where [Markdown](https://wikipedia.org/wiki/Markdown) became a standard
for [README](https://wikipedia.org/wiki/README) files, that's why we talk about **README.md**.

However professional developers forging commercial products with closed (private) source code
may doubt about usefulness of the README files.
"We know our code, we do not need to open it" - may they say.
And will be wrong because basic principles of the Source Code are the same -
the Source code is being developed by people for people, and people should know about
What is this Source Code and How to use it, no matter free it or commercial, open or closed.

All software companies care about maintainability trying minimize expenses for the Source Code support.
That's why successful onces always have internal documentation where README file is the simples one.
README files are always useful for newcomers and just for people who never seen some particular
modules, libraries, parts of the code.

However README files must be written wisely, not formally.
They will be really useful only if they answer to the questions which are actually asked.
So [writing a README is an Art](https://github.com/noffle/art-of-readme).
Some guys even think that the
[README is the most important file](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html)
in your project.

# How?

How to make README file most useful?
How good README file should look like?

- What file format to use?
- Which sections should it contain?
- Which rules to follow when writing?

### File format

There are many formats for README.
Historically a lot of projects have README in a plain TXT format (README.txt).
Well, it is a bit old-fashioned but always works.
Other formats might be HTML, [RST](https://wikipedia.org/wiki/ReStructuredText),
[Textile](https://textile-lang.com/), [RDoc](https://ruby.github.io/rdoc/),
[AsciiDoc](http://asciidoc.org/), and some others, sometimes even PDF, DOC or RTF.
However they are not so popular usually due to their complexity.
Today the most popular format for README is Markdown, and here is why:

1. Markdown format is *very simple*.<br>
   You can [learn it in 10 min](https://commonmark.org/help/tutorial/)
   or even [in 60 sec](https://commonmark.org/help/) ☺
2. Markdown can and should! be read as *plain text*.
3. At the same time Markdown provides good *formatting possibilities*,<br>
   like multilevel text structure, paragraphs, lists, tables, images, quotes, links etc
4. It also supports *embedded HTML*.<br>
   So you can use the power of HTML markup if pure Markdown is not enough.
5. README.md became a *standard de-facto* for the source code organization,
   especially for Open Source projects.<br>
   Today README.md is being considered as a default README file.
6. README.md is automatically rendered by the most of *Git repo* viewers like<br>
   [GitHub](https://github.com), [GitLab](https://gitlab.com),
   [Gitiles](https://gerrit.googlesource.com/gitiles/) etc

Despite the popularity Markdown is still not standardized officially.
There is a number of variants of Markdown implementations which provide additional
formatting possibilities (we can consider them as extensions) which called flavors.
Note that the core specification of all Markdown variants is the same,
so 90% of all Markdown flavors are compatible.
Besides Markdown is still plain text.

The following Markdown flavors are recommended since they are the most popular:
* [CommonMark](https://commonmark.org/) - strongly defined, highly compatible specification of Markdown
* [GitHub Flavored Markdown](https://github.github.com/gfm/)
  ([short version](https://help.github.com/articles/basic-writing-and-formatting-syntax))
* [GitLab Flavored Markdown](https://docs.gitlab.com/ce/user/markdown.html)
* [Gitiles Markdown](https://gerrit.googlesource.com/gitiles/+/HEAD/Documentation/markdown.md)

You can also take a look at long list of
[Markdown Flavors](https://github.com/commonmark/commonmark-spec/wiki/Markdown-Flavors).

### Sections

What kind of information we usually want from README file?<br>
First we usually ask - `What is it?`<br>
When we find the answer we usually decide to use it or forget it.<br>
So the next question is usually - `How to use it?`<br>
Since it is usually the Source Code then next we ask - `How to build it?`<br>
Then we may go deeper and ask some more question:<br>
`How to install?`, `How to test?`, `What are these files?`, `How it works?`.

Sections of our README.md file should reflect these questions.
So we can define very basic sections like the following:

1. **The title**
2. **Description**
3. **File structure**
4. **Requirements**
5. **How to build / Building**
6. **How to test / Testing**
7. **How to install / Installation**
8. **How to use / Usage**

Sometimes README files may also contain the following optional sections:

* **How it works** - however the description might be long,
  in this case it would be better to provide extensive documentation in `docs` folder
* **Versions / Release History** - sure, if the list of releases is not long,
  otherwise you can put it in special `CHANGELOG` file
* **How to contribute** - you can add this too,
  but probably standard `CONTRIBUTING.md` file would be better
* **License** - hm... it would be better to use `LICENSE` file
* **Authors** - absolutely good idea!
* **Acknowledgments / Credits** - no problem ☺, if you want

### Rules

Here are some basic rules which are recommended to follow when writing README.md:

1. Always make sure that README.md can be normally read as plain text.<br>
   Just use `cat README.md`
2. Try to avoid long lines, break them with word-wrap.<br>
   Recommended max line length is 100.<br>
   This is important to correctly display your README.md as a plain text!
3. Follow [CommonMark](https://commonmark.org/) specification to ensure
   compatibility among various Markdown viewers
4. Use text editors which have syntax highlighting for Markdown -
   it will help you to check Markdown syntax on-the-fly
   and also see better the structure of your README.md
5. Be careful when using specific "flavored" Markdown formats
   - make sure your README.md can be correctly shown as a plain text
   - check that README.md is correctly rendered by the target viewer
   - check also that README.md can be rendered by other viewers (GitHub, GitLab etc)
   - anyway, try to follow [CommonMark](https://commonmark.org/) spec
6. Do not use tab symbols - they are just useless in Markdown

## Template

The following template can be used when writing README.md file:
```md
The title
=========

Description
-----------

What is this? What is this for?
Abbreviations etc

Folder structure
----------------

Describe files and folders.
Use list of files with short description.

Requirements
------------

Which Operating Systems are supported?
Which packages should be preinstalled before you build the product?

How to build?
-------------

Build instructions, e.g. `make`

How to test?
------------

How to run tests?
Yes, you have to have tests!

How to install?
---------------

How to install the product (tool/library) we just built?
Describe install options if any.
This section is optional since not all products should be installed.

How to use?
-----------

How the product (tool/library) can be used?
Describe use-cases, command-line options if any.
Add usage examples.
```

## Example

```md
Foobar
======

Foobar is a library and a tool which implement simple functionality.
It does something with something to produce interesting artifacts.
The library can be used as a shared object with simple C API.
The tool is a conventional linux command line (CLI) application.

Folder structure
----------------

- `Makefile`           - simple Makefile to build, clean etc
- `inc/api.h`          - Foobar API
- `src/api.cc`         - implementation of Foobar API
- `src/application.h`  - Application class
- `src/application.cc` - implementation of Application class
- `src/function.h`     - data structures and constants
- `src/function.c`     - implementation of the functionality
- `src/example.c`      - simple C example of shared library usage
- `src/main.cc`        - "main" function of CLI
- `test/test.h`        - Test class
- `test/test.cc`       - basic tests

Requirements
------------

At the moment only **Ubuntu** is supported.
To build Foobar install the following packages:
`sudo apt-get install build-essential libtool gcc g++`

How to build?
-------------

Use `make` to build all targets.

### Targets:

Target       | Description
------------ | -----------
foobar       | Build command line (CLI) tool
libfoobar.so | shared library, implements C API
libfoobar.a  | static library
test         | test binary
example      | C example

Type `make help` to see additional options.

How to test?
------------

Run `make run-test` to build and run simple test.

When test is built you can also run `./test`.

See also available options `./test -h`.

How to use?
-----------

Foobar can be used as a command line tool.
Type `./foobar -h` to see available options.

Foobar can also be used as static (libfoobar.a) or shared (libfoobar.so) library.
In your C or C++ code include *api.h* file where *foobar()* function is declared.
In case of shared library you should load it using *dlopen* and *dlsym* functions.
See simple C example *example.c*.
```

## Output

When rendered by GitLab, GitHub, Gitiles etc it will look like the following:

> Foobar
> ======
>
> Foobar is a library and a tool which implement simple functionality.
> It does something with something to produce interesting artifacts.
> The library can be used as a shared object with simple C API.
> The tool is a conventional linux command line (CLI) application.
>
> Folder structure
> ----------------
>
> - `Makefile`           - simple Makefile to build, clean etc
> - `inc/api.h`          - Foobar API
> - `src/api.cc`         - implementation of Foobar API
> - `src/application.h`  - Application class
> - `src/application.cc` - implementation of Application class
> - `src/function.h`     - data structures and constants
> - `src/function.c`     - implementation of the functionality
> - `src/example.c`      - simple C example of shared library usage
> - `src/main.cc`        - "main" function of CLI
> - `test/test.h`        - Test class
> - `test/test.cc`       - basic tests
>
> Requirements
> ------------
>
> At the moment only **Ubuntu** is supported.
> To build Foobar install the following packages:
> `sudo apt-get install build-essential libtool gcc g++`
>
> How to build?
> -------------
>
> Use `make` to build all targets.
>
> ### Targets:
>
> Target       | Description
> ------------ | -----------
> foobar       | Build command line (CLI) tool
> libfoobar.so | shared library, implements C API
> libfoobar.a  | static library
> test         | test binary
> example      | C example
>
> Type `make help` to see additional options.
>
> How to test?
> ------------
>
> Run `make run-test` to build and run simple test.
>
> When test is built you can also run `./test`.
>
> See also available options `./test -h`.
>
> How to use?
> -----------
>
> Foobar can be used as a command line tool.
> Type `./foobar -h` to see available options.
>
> Foobar can also be used as static (libfoobar.a) or shared (libfoobar.so) library.
> In your C or C++ code include *api.h* file where *foobar()* function is declared.
> In case of shared library you should load it using *dlopen* and *dlsym* functions.
> See simple C example *example.c*.

## Editor

Another question - which editor to use when writing README.md?

Basically Markdownd format is just a plain text, so we can use any source code editor.
However almost all popular code editors have syntax highlighting and rendering preview
support for Markdown through plugins and extensions.

For example the following is taken from the article
[The Best Markdown Editor for Linux](https://www.sitepoint.com/the-best-markdown-editor-for-linux/):

* [Vim](http://www.vim.org/) has a
  [Vim-Markdown plugin](https://github.com/plasticboy/vim-markdown)
  that features syntax highlighting and folding.
* [Emacs](https://www.gnu.org/software/emacs/) has a
  [Markdown Mode for Emacs](http://jblevins.org/projects/markdown-mode/)
  package that includes shortcut keys and syntax highlighting.
* [Eclipse](https://eclipse.org/) has the
  [Markdown Text Editor plugin](https://marketplace.eclipse.org/content/markdown-text-editor)
  which includes a document outline, folded sections, preview, export to HTML,
  task tags, word wrap and paragraph formatting.
* [Visual Source Code](https://code.visualstudio.com/)
  offers syntax highlighting and
  [extensions for Markdown](https://code.visualstudio.com/docs/languages/markdown).
* [Atom](https://atom.io/) supports Markdown out of the box,
  with features like syntax highlighting and preview.
  This functionality can be expanded by several community-generated packages, including
  [Markdown-Writer](https://atom.io/packages/markdown-writer),
  [Markdown-Scroll-Sync](https://atom.io/packages/markdown-scroll-sync) and
  [Markdown-Format](https://atom.io/packages/markdown-format).
* [Sublime Text](https://www.sublimetext.com/) has packages for
  [Markdown syntax highlighting](https://packagecontrol.io/packages/MarkdownEditing) and
  [Markdown preview](https://packagecontrol.io/packages/MarkdownPreview)
* [Spacemacs](http://spacemacs.org/) has a
  [Markdown layer](http://spacemacs.org/layers/+lang/markdown/README.html)
  to add Markdown support.
* [Brackets](http://brackets.io/) has a
  [Markdown extension](https://github.com/gruehle/MarkdownPreview)
  with syntax highlighting and a preview pane.
* [Bluefish](http://bluefish.openoffice.nl/index.html)
  includes syntax highlighting for Markdown files.
* [Gedit](https://wiki.gnome.org/Apps/Gedit), the Gnome text editor, offers the
  [gedit-markdown plugin](https://github.com/jpfleury/gedit-markdown)
  with live Markdown preview and syntax highlighting.
* [Kate](https://kate-editor.org/), the KDE text editor, supports Markdown syntax highlighting.

There are similar articles about Markdown editors
for [Mac](https://www.sitepoint.com/the-best-markdown-editors-for-mac/)
and [Windows](https://www.sitepoint.com/best-markdown-editors-windows/)

## Links

If you want read more about README there are some articles listed below:

* [Make a README](https://www.makeareadme.com/)
* [Your Project is Great, So Let's Make Your README Great Too](https://embeddedartistry.com/blog/2017/11/20/your-readme-probably-sucks-its-time-to-make-it-better)
* [A Beginners Guide to writing a Kickass README](https://medium.com/@meakaakka/a-beginners-guide-to-writing-a-kickass-readme-7ac01da88ab3)
* [Drupal README template](https://www.drupal.org/docs/develop/documenting-your-project/readme-template)
* [Readme Driven Development](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html)
* [Standard Readme](https://github.com/RichardLitt/standard-readme)
* [Art of README](https://github.com/noffle/art-of-readme)
