# The Structure of a LATEX Document
<!-- chapter 2 -->

This chapter explains how the general principle of separation between layout and structure is
implemented in LaTeX. (This separation helps the user concentrate on content rather than having to
worry about layout issues.)

Sections: 

* `The structure of a source file`: how document-class files, packages, options, and preamble
  commands can affect the structure and layout of a document

* `Sectioning commands`: how sectioning commands and their arguments define a hierarchical
  structure, how they generate numbers for titles, and how they produce running heads and feet
  
    - different ways of typesetting section titles are presented with the help of examples
    - it is shown how information written to the table of contents can be controlled and how the
      look of this table, as well as that of the lists of tables and figures, can be customized

* `Combining several files`: introduces LaTeX commands for managing cross-references and their
  scoping rules


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## The structure of a source file
<!-- 2.1 -->

Documents for different purposes may need different logical structures, i.e. different commands and
environments. We say that a document belongs to a **document class** having the same general
structure (but not necessarily the same typographical appearance). Start your LaTeX file with a
`\documentclass` command, where the mandatory parameter specifies the name of the document class.
The document class defines the available logical commands and environments (for example, `\chapter`
in the report class) as well as a default formatting for those elements.

The very first line in a file might look like: 

```latex
\documentclass[utf8]{my_class}
```

An optional argument allows you to modify the formatting of those elements by supplying a list of
class options. For example, `11pt` is an option recognized by most document classes that instructs
LaTeX to choose eleven point as the basic document type size.

**Packages and package options**

Many LaTeX commands described in this book are not specific to a single class but can be used with
several classes. A collection of such commands is called a **package** and you inform LaTeX about
your use of certain packages in the document by placing one or more `\usepackage` commands after
`\documentclass`. 

Just like the `\documentclass` declaration, `\usepackage` has a mandatory argument consisting of the
name of the package and an optional argument that can contain a list of **package options** that
modify the behavior of the package.

* The document classes and the packages reside in external files with the extensions `.cls` and
  `.sty`, respectively.

* Code for options is sometimes stored in external files (in the case of class files with the
  extension `.clo`) but is normally directly specified in the class or package file. However, in
  case of options, the file name can differ from the option name. For example, the option `11pt` is
  related to `size11.clo` when used in the article class and to `bk11.clo` inside the `book`
  class.

**The document preamble**

Commands placed between `\documentclass` and `\begin{document}` are in the so-called **document
preamble**. All **style parameters** *must* be defined in this preamble, either in package or class
files or directly in the document before the `\begin{document}` command---which would set the
values for some of the global parameters. 

A typical document preamble could look similar to the following:

```latex
\documentclass[twocolumn,a4paper]{article}
\usepackage{multicol}
\usepackage[german,french]{babel}
\addtolength\textheight{3\baselineskip} % i
% i: the default height of the text body was enlarged by three lines for this document

\begin{document}
```

<!-- The list below "splits an infinitive around a colon". Oxford Style allows it. (page 301) -->
To modify the layout of a document, you have several possibilities:

* change the standard settings for parameters in a class file by options defined for that class
* add one or more packages to your document and make use of them
* change the standard settings for parameters in a package file by options defined for that package
* write your own local packages containing special parameter settings and load them with
  `\usepackage` after the package or class they are supposed to modify (as explained in the next
  section)
* make final adjustments inside the preamble

### Processing of options and packages
<!-- 2.1.1 -->

LaTeX makes a clear distinction between

* **declared options** (of a class *or* package), which can be either
    - properties of the whole document (when used in `\documentclass`), or
    - properties of individual packages (if specified in `\usepackage`)

* *general-purpose package files* (packages specified using the `\usepackage` command)

All options to `\documentclass` (both declared and not declared) are automatically passed as class
options to all `\usepackage` declarations. Thus, if a package file loaded with a `\usepackage`
declaration **recognizes (i.e. declares)** some of the class options, it can take appropriate
actions. If not, the class options will be ignored while processing that package.

Because all options have to be defined inside the class or package file, their actions are under the
control of the class or package. This means that the actions are not quite under your control so
the order you enter the options in the optional argument of `\documentclass` or `\usepackage` is
(usually) irrelevant.

* You can specify options in a `\usepackage` command only if these options are declared by the
  package. Otherwise, you will receive an error message, informing you that your specified option
  is unknown to the package in question

* Options specified to the `\documentclass` which are not declared by the class, will be assumed to
  be a "global" options

**Example**

Specifying `german` as a class option will pass `german` to all loaded packages and thus will be
processed by those packages that declare it (i.e. that have it as an valid option). This syntax can
can be used to shorten the `\usepackage` declaration.

```latex
\documentclass[german]{book} % this passes "german" as a global option to the class
\usepackage{babel,varioref,multicol,epic}

% this example assumes that we want "german" to affect the functioning of babel and varioref, and
% that neither multicol nor epic will change their behaviour
```

When the `\begin{document}` is reached, all global options are checked to see whether each has been
used by at least one package; if not, a warning message is displayed. It is usually a spelling
mistake if your option name is never used; another possibility is the removal of a `\usepackage`
command loading a package that used this option previously.

**Making Modifications**

If you want to make some modifications to a document class or a package (for example, changing
parameter values or redefining some commands), you should put the relevant code into a separate file
with the extension `.sty`. Then load this file with a `\usepackage` command after the package whose
behavior you wish to modify (or the document class, if your modifications concern class issues).

Alternatively, you can insert the modifications directly into the preamble of your document. In that
case, you may have to bracket them with `\makeatletter` and `\makeatother` if they contain internal
LaTeX commands (i.e. those with an `@` sign in their names). For more details see the discussion on
page 843 concerning internal commands in the preamble.

<!-- continue re-reading here -->
<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Splitting the source file into parts

### Partial processing

LaTeX source documents can be conveniently split into several parts by using `\include` commands. Moreover, documents can be reformatted piecewise by specifying, as arguments of an `\includeonly`, command only those files LaTeX has to reprocess.

For the other files that are specified in `\include` statements, the counter[^counter] information will be read from the corresponding `.aux` files **as long as** they have been generated during a previous run. If the information in the `.aux` files is up-to-date, it is possible to process only part of a document and have all counters, cross-references, and pages be corrected in the reformatted part. However, if one of the counters (including the page number for cross-references) changes in the reprocessed part, then the complete document might have to be rerun to get the index, table of contents, and bibliographic references consistently correct.

[^counter]: i.e. counters for pages, chapters, tables, figures, equations, etc.

In the following example, the user **only** wants to reprocess files `chap1.tex` and `appen1.tex`:

```latex
\documentclass{book} % the document class ‘‘book''
\includeonly{chap1,appen1} % only include chap1 and appen1
\begin{document}
\include{chap1}  % input chap1.tex
\include{chap2}  % input chap2.tex
\include{chap3}  % input chap3.tex
\include{appen1} % input appen1.tex
\include{appen2} % input appen2.tex
\end{document}
```

Be aware that LaTeX only issues a warning message like "No file xxx.tex" when it cannot find a file
specified in an `\include` statement, not an error message, and continues processing.

Note that each document part loaded via `\include` starts on a new page and finishes by calling `\clearpage`; thus, ﬂoats contained therein will not move outside the pages produced by this part. ( So natural candidates for `\include` are whole chapters of a book but not necessarily small fractions of text.)

### Interactive Inclusion

If you intend to work with `\include` commands, consider using the small package `askinclude` created by Pablo Straub. It interactively asks you which files to include. You can then specify the files as a comma-separated list (i.e. what you would put into the `\includeonly` argument). If the Enter button is pressed in response, then the files from the previous run are included automatically (except on the first run, where this response means to include all files). If the answer is a `*`, then all files are included; a `-` means no files should be included. This way you do not have to modify your master source to process different parts of your document (a very useful feature during the production of this book).

An extension to the `\include` mechanism is provided by the package `excludeonly` (see page 20 for more information).

<!-- two more subsections with probably arcane information -->


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Sectioning Commands

A basic document consists of a title, sections (with probably a multilevel nested substructure), and a list of references. To describe such a structure following commands are used

* the title-generating command \maketitle
* sectioning commands such as \section and \subsection
* the `thebibliography` environment

Longer works (such as reports, manuals, and books) start with more complex title information, are subdivided into chapters (and parts), provide cross-reference information (table of contents, list of figures, list of tables, and indexes), and probably have appendices. In such a document you can easily distinguish the front matter, body, and back matter.

* In the `book` class these three parts can be explicitly marked up using the commands \frontmatter,
  \mainmatter , and \backmatter.

* In other classes you often find only the command \appendix , which is used to separate the body matter from the back matter.

In the front matter the so-called starred form of the \section or `\chapter` sectioning command is normally used. This form suppresses the numbering of a heading. Sectional units with fixed names, such as "Index" and "Preface", are usually not numbered. (In the standard classes, the commands \tableofcontents , \listoftables , and \listoffigures , and the `theindex` and `thebibliography` environments internally invoke the command (\section or `\chapter`) using their starred form.)

Standard LaTeX provides the set of sectioning commands shown in Table 2.1.

<!-- The \chapter command defines level zero of the hierarchical structure of a document, \section defines level one, and so on, whereas the optional \part command defines the level minus one (or zero in classes that do not define \chapter). -->

Not all of these commands are defined in all document classes. The `article` class does not have `\chapter` and the `letter` class does not support sectioning commands at all. It is also possible for a package to define other sectioning commands, allowing either additional levels or variants for already supported levels.

Generally, the sectioning commands automatically perform one or more of the following typesetting actions:

* Produce the heading number reﬂecting the hierarchical level.
* Store the heading as an entry for a table of contents (into the `.toc` file).
* Save the contents of the heading to be (perhaps) used in a running head and/or foot.
* Format the heading.

All sectioning commands have a common syntax as exemplified here by the \section command:

```latex
\section*{title}            % i
\section[toc-entry]{title}  % ii

% i: suppresses the numbering for a title and does not produce an entry in the table of contents or
% the running head

% ii: used when the printed title is different from the text that will go in the table of contents,
% the running head, and/or foot. If this variant is used, numbering depends on the current value of
% the counter secnumdepth
```



<!-- continue at pdf 53 page 24 Numbering headings -->
