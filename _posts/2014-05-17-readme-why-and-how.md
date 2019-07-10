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

Despite the popularity Markdown is still not standardized.
There is a number of variants of Markdown which provide additional formatting possibilities
(we can consider them as extensions) which called flavors.
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

What information we want to get from README file?

* How to contribute? - CONTRIBUTING.md
* License? - LICENSE
* How it works? - docs
* Versioning? Release History?
* Authors?
* Acknowledgments?

### Rules

* You can use "flavored" Markdown formats but make sure that
  your README.md can be correctly shown as a plain text!
* Recommended Max line length: 100.
  This is important to correctly display your README.md as a plain text!
* Do not use tab symbols - they are just useless in Markdown

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
Something
=========

This is a library and a tool which implement simple functionality.
It does something with something to produce interesting artifacts.
The library can be used in as a shared object with simple C API.
The tool is a conventional linux command line (CLI) application.

Folder structure
----------------

- `Makefile`           - simple Makefile to build, clean etc
- `inc/api.h`          - C API
- `src/api.cc`         - implementation of C API
- `src/application.h`  - Application class
- `src/application.cc` - implementation of Application class
- `src/function.h`     - data structures and constants
- `src/function.c`     - implementation of the functionality
- `src/example.c`      - simple C example of shared library usage
- `src/main.cc`        - "main" function
- `test/test.h`        - Test class
- `test/test.cc`       - basic tests

Requirements
------------

At the moment only **Ubuntu** is supported.
To build the product install the following packages:
`sudo apt-get install build-essential libtool gcc g++`

How to build?
-------------

Use `make` to build all targets.

### Targets:

   Target | Description
--------- | -----------
tool      | command line (CLI) tool
liblib.so | shared library, implements C API
liblib.a  | static library
test      | test binary
example   | C example

Type `make help` to see additional options.

How to test?
------------

Run `make run-test` to build and run simple test.

When test is built you can run `./test`.

See also available options `./test -h`.

How to use?
-----------

The something can be used as a command line tool.
Type `./tool -h` to see available options.

It can be also used as static (liblib.a) or shared (liblib.so) library.
In your C or C++ file include *api.h* file where *something()* function is declared.
In case of shared library you should load it using *dlopen* and *dlsym* functions.
See simple C example *example.c*.
```

## Output

When rendered by GitLab, GitHub, Gitiles etc it will look like the following:

> Something
> =========
>
> This is a library and a tool which implement simple functionality.
> It does something with something to produce interesting artifacts.
> The library can be used in as a shared object with simple C API.
> The tool is a conventional linux command line (CLI) application.
>
> Folder structure
> ----------------
>
> - `Makefile`           - simple Makefile to build, clean etc
> - `inc/api.h`          - C API
> - `src/api.cc`         - implementation of C API
> - `src/application.h`  - Application class
> - `src/application.cc` - implementation of Application class
> - `src/function.h`     - data structures and constants
> - `src/function.c`     - implementation of the functionality
> - `src/example.c`      - simple C example of shared library usage
> - `src/main.cc`        - "main" function
> - `test/test.h`        - Test class
> - `test/test.cc`       - basic tests
>
> Requirements
> ------------
>
> At the moment only **Ubuntu** is supported.
> To build the product install the following packages:
> `sudo apt-get install build-essential libtool gcc g++`
>
> How to build?
> -------------
>
> Use `make` to build all targets.
>
> ### Targets:
>
>    Target | Description
> --------- | -----------
> tool      | command line (CLI) tool
> liblib.so | shared library, implements C API
> liblib.a  | static library
> test      | test binary
> example   | C example
>
> Type `make help` to see additional options.
>
> How to test?
> ------------
>
> Run `make run-test` to build and run simple test.
>
> When test is built you can run `./test`.
>
> See also available options `./test -h`.
>
> How to use?
> -----------
>
> The something can be used as a command line tool.
> Type `./tool -h` to see available options.
>
> It can be also used as static (liblib.a) or shared (liblib.so) library.
> In your C or C++ file include *api.h* file where *something()* function is declared.
> In case of shared library you should load it using *dlopen* and *dlsym* functions.
> See simple C example *example.c*.

## Links

If you want read more about README there are some articles listed below:

* [Make a README](https://www.makeareadme.com/)
* [Your Project is Great, So Let's Make Your README Great Too](https://embeddedartistry.com/blog/2017/11/20/your-readme-probably-sucks-its-time-to-make-it-better)
* [A Beginners Guide to writing a Kickass README](https://medium.com/@meakaakka/a-beginners-guide-to-writing-a-kickass-readme-7ac01da88ab3)
* [Drupal README template](https://www.drupal.org/docs/develop/documenting-your-project/readme-template)
* [Readme Driven Development](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html)
* [Standard Readme](https://github.com/RichardLitt/standard-readme)
* [Art of README](https://github.com/noffle/art-of-readme)
