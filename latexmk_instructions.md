# Instructions for Latexmk

These are just personal notes, much is missing! 
See all this content and more on the [homepage][homepage].

Latexmk (whose current released version is 4.86a dated 27 December 2024) is a perl script for
running LaTeX the correct number of times to resolve cross references, etc; it also runs auxiliary
programs (bibtex, makeindex if necessary, and dvips and/or a previewer as requested). 

It has a number of other useful capabilities, for example to start a previewer and then run latex
whenever the source files are updated, so that the previewer gives an up-to-date view of the
document. 

Here is the [documentation in plain text format][doc_plain_text], and 
in [pdf format][doc_pdf_format].

## Introduction

Latexmk completely automates the process of compiling a LaTeX document. 

Essentially, it determines dependencies automatically and has some other very useful features.

A very annoying complication handled very reliably by latexmk, is that LaTeX is a multiple pass
system. On each run, LaTeX reads in information generated on a previous run, for things like cross
referencing and indexing. In the simplest cases, a second run of LaTeX suffices, and often the log
file contains a message about the need for another pass. However, there is a wide variety of add-on
macro packages to LaTeX, with a variety of behaviors. The result is to break simple-minded
determinations of how many runs are needed and of which programs. Latexmk has a highly general and
efficient solution to these issues. The solution involves retaining between runs information on the
source files, and a symptom is that latexmk generates an extra file (with extension `.fdb_latexmk`,
by default) that contains the source file information.

In its basic mode of operation latexmk is given the name of the primary source file for a document,
and it issues the appropriate sequence of commands to generate a .dvi, .ps, .pdf and/or hardcopy
version of the document.

By default latexmk will run the commands necessary to generate a .dvi file, which copies the
behavior of earlier versions when only latex was available.

Latexmk can also be set to run continuously with a suitable previewer. In that case the latex
program (or one of its relatives), etc, are rerun whenever one of the source files is modified, and
the previewer automati- cally updates the on-screen view of the compiled document.

## Latexmk Options and Arguments on Command Line 

In general the command line to invoke latexmk has the form: `latexmk [options] [file]`.

Run latexmk with `-showextraoptions` to get a list of the options that latexmk accepts and that are
simply passed through to `*latex`. (See also the explanation of the `-showextraoptions` option for
more information.)


* `-pdf`: generate pdf version of document using pdflatex. (And turn off any incompatible requests.)

* `-silent`: run commands silently, i.e., with options that reduce the amount of diagnostics
  generated ... Also reduce the number of informational messages that latexmk itself generates. To
  change the options used to make the commands run silently, you need to configure latexmk with
  changed values of its configuration variables, the relevant ones being $bibtex_silent_switch,
  $biber_silent_switch, $dvipdf_silent_switch, $dvips_silent_switch, $dvilualatex_silent_switch,
  $latex_silent_switch, $lualatex_silent_switch $makeindex_silent_switch,
  $pdflatex_silent_switch, and $xelatex_silent_switch

* `-verbose`: opposite of `-silent`. This is the default setting.


[homepage]: [https://www.cantab.net/users/johncollins/latexmk/index.html]

[doc_plain_text]: https://www.cantab.net/users/johncollins/latexmk/latexmk-486a.txt

[doc_pdf_format]: https://www.cantab.net/users/johncollins/latexmk/latexmk-486a.pdf

<!-- possibly useful notes in page below -->
<!-- https://mgeier.github.io/latexmk.html -->
