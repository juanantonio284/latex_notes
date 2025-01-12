<!-- tutorial 1 -->
# Simple Typesetting

## Spaces

In traditional typesetting, a little extra space is added to periods which end sentences and TeX
also follows this custom. But how does TeX know whether a period ends a sentence or not? It assumes
that every period not following an upper case letter ends a sentence. 

### Extra space after period needed (sentence ends with uppercase letter)

There are instances where a sentence ends in an upper case letter. **Add an extra space after the
period with `\@`.**

For example, consider the following

```
Carrots are good for your eyes, since they contain Vitamin A. Have you ever seen a rabbit
wearing glasses?
```
The right input to produce this is

```Latex
Carrots are good for your eyes, since they contain Vitamin A\@. Have you ever seen a rabbit wearing
glasses?
```

### Extra space after period not needed (period does not mark end a sentence)

There are instances where a period following a lowercase letter does not end a sentence. **Enter an
escaped space `\ ` so that the compiler focuses on that and not on the period.**
<!-- **Remove the extra space with a backslash and a space `\ `. (This is an escaped space.)** -->

For example:

```
The numbers 1, 2, 3, etc. are called natural numbers. According to Kronecker, they were made
by God; all else being the work of Man.
```

To produce this (without extra space after etc.) the input should be

```Latex
The numbers 1, 2, 3, etc.\ are called natural numbers. According to Kronecker, they were made by
God; all else being the works of Man.
```

### Space needed (after a command the following space is not inserted at all)

TeX gobbles up all spaces after a command. **Enter an escaped space `\ ` so that the compiler
focuses on that and not on the command.**

For example, to properly display the sentence: `I think LaTeX is fun` you should write:
```Latex 
I think \LaTeX\ is fun
```

<!-- ## Dashes -->
<!-- ## Accents -->
<!-- ## Special symbols -->
<!-- ## Text alignment -->

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
# Fonts

The actual letters and symbols (collectively called type) that LaTeX (or any other typesetting
system) produces are characterized by their style and size. For example, in this book emphasized
text is given in italic style and the example inputs are given in typewriter style. We can also
produce smaller and bigger types. A set of types of a particular style and size is called a font.

## Type style

In LaTeX, a type style is specified by family, series, and shape. Any type style in the output is a
combination of these three characteristics.

<!-- See table 1.1 on page 14 -->

### Commands vs. declarations

Each of these type style changing commands has an alternate form as a declaration.

A command is `\textbf{boldface}`, a declaration is `{\bfseries boldface}`. Declarations seem to end
in "shape", "series", or "family"—e.g. `upshape`, `mdseries`, `ttfamily`. (See table on page 15)

`\bfseries{triangle}` would not work (both the declaration and the text need to be in the braces).

## Type size

Traditionally, type size is measured in (printer) points. The default type that TeX produces is of
10 pt size. There are 10 **declarations** provided in LaTeX for changing the type size:

```
{\tiny size}
{\scriptsize size}
{\footnotesize size}
{\small size}
{\normalsize size}
{\large size}
{\Large size}
{\LARGE size}
{\huge size}
{\Huge size}
```

Note that the `\normalsize` corresponds to the size we get by default and the sizes form an ordered
sequence with `\tiny` producing the smallest and `\Huge` producing the largest. Unlike the style
changing commands, there are no command-with-one-argument forms for these declarations.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- tutorial 2 -->
# The Document

## \documentclass

In addition to specifying the type of document (which we must do, since LaTeX has no default
document class), we can also specify some options which modify the overall appearance that the
document has by default. Thus the actual syntax of the `\documentclass` command is `\documentclass
[options]{class}`

Note that options are given in square brackets and not braces. (This is often the case with LaTeX
commands—options are specified within square brackets, after which mandatory arguments are given
within braces.)

### Font size

We can select the size of the font for the normal text in the entire document with one of the
options 10pt 11pt 12pt. Thus we can say `\documentclass[11pt]{article}` to set the normal text in
our document to 11pt size. (The default is 10pt).

### Paper size

We know that LaTeX has its own method of breaking lines to make paragraphs. It also has methods to
make vertical breaks to produce different pages of output. For these breaks to work properly, it
must know the width and height of the paper used. The various options for selecting the paper size
are given below:

|    **command**   |   **size**   |
|:----------------:|:------------:|
|   `letterpaper`  |   11×8.5 in  |
|   `legalpaper`   |   14×8.5 in  |
| `executivepaper` | 10.5×7.25 in |
|     `a4paper`    |  20.7×21 in  |
|     `a5paper`    |  21×14.8 in  |
|     `b5paper`    |  25×17.6 in  |

Normally, the longer dimension is the vertical one—that is, the height of the page. The default is
letterpaper.

### Page formats

There are options for setting the contents of each page in a single column (as is usual) or in two
columns (as in most dictionaries). This is set by the options: `onecolumn` and `twocolumn` (the
default is `onecolumn`).

There is also an option to specify whether the document will be finally printed on just one side of
each paper or on both sides. The names of the options are `oneside` and `twoside`. One of the
differences is that with the `twoside` option, page numbers are printed on the right on
odd-numbered pages and on the left on even numbered pages, so that when these printed back to back,
the numbers are always on the outside, for better visibility. The default is `oneside` for article,
report and letter and `twoside` for book.

<!-- etc -->

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## \pagestyle

Having decided on the overall appearance of the document through the `\documentclass` command with
its various options, we next see how we can set the style for the individual pages. 

In LaTeX parlance, each page has a "head" and "foot" usually containing such information as the
current page number or the current chapter or section. This is set by the command `\pagestyle{...}` 
where the mandatory argument can be any one of the following styles: `plain`, `empty`, `headings`,
`myheadings`.

The behavior pertaining to each of these is given below:

* `plain`: the page head is empty and the foot contains just the page number, centered with respect
  to the width of the text. (This is the default for the `article` class if no `\pagestyle` is
  specified in the preamble.)

* `empty`: both the head and foot are empty. In particular, no page numbers are printed.

* `headings`: this is the default for the `book` class. The foot is empty and the head contains the
  page number and names of the chapter section or subsection, depending on the document class and
  its options as given below:
  
|   **Class**  | **Option** | **Left Page** | **Right Page** |
|:------------:|:----------:|:-------------:|:--------------:|
| book, report |  one-sided |       —       |     chapter    |
| book, report |  two-sided |    chapter    |     section    |
|    article   |  one-sided |       —       |     section    |
|    article   |  two-sided |    section    |   subsection   |


* `myheadings` The same as headings, except that the 'section' information in the head are not
  predetermined, but to be given explicitly using the commands `\markright` or `\markboth`.

Moreover, we can customize the style for the current page only using the command `\thispagestyle
{style}` where style is the name of one of the styles above. For example, the page number may be
suppressed for the current page alone by the command `\thispagestyle{empty}`. (Note that only the
printing of the page number is suppressed. The next page will be numbered with the next number and
so on.)


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## \pagenumbering

The style of page numbers can be specified by the command `\pagenumbering{...}` The possible
arguments to this command and the resulting style of the numbers are given below:

* `arabic`: Indo-Arabic numerals
* `roman`: lowercase Roman numerals
* `Roman`: upper case Roman numerals
* `alph`: lowercase English letters
* `Alph`: uppercase English letters

The default value is arabic. This command resets the page counter. 

Thus for example, to number all the pages in the ‘Preface’ with lowercase Roman numerals and the
rest of the document with Indo-Arabic numerals, declare `\pagenumbering{roman}` at the beginning of
the Preface and issue the command `\pagestyle{arabic}` immediately after the first `\chapter`
command. We can make the pages start with any number we want by the command `\setcounter{page}
{number}` where number is the page number we wish the current page to have.

## \setlength

Each page that LaTeX produces consists not only of a head and foot as discussed above but also a
body containing the actual text. In formatting a page, LaTeX uses the width and heights of these
parts of the page and various other lengths such as the left and right margins. The values of these
lengths are set by the paper size options and the page format and style commands. 

For example, the page layout with values of these lengths for an odd page and even in this book are
separately shown below. These lengths can all be changed with the command `\setlength`. For
example, `\setlength{\textwidth}{15cm}` makes the width of text 15 cm. The package `geometry` gives
easier interfaces to customize page format.

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Parts of a document

Documents (especially longer ones) are divided into chapters, sections and so on. There may be a
title part (sometimes even a separate title page) and an abstract. All these require special
typographic considerations and LaTeX has a number of features which automate this task.

### Title

The "title" is printed in a separate page for the document classes `book` and `report` and in the
first page of the document for the class `article`. (Also recall that this behavior can be modified
by the options `titlepage` or `notitlepage`.)

To produce a title, we make use of the commands: 

```Latex
\title{document name}
\author{author names}
\date{date text}
\maketitle % must issue this command to actually typeset the title
```

By default, all entries produced by these commands are centered on the lines in which they appear.
If a title text is too long to fit in one line, it will be broken automatically. However, we can
choose the break points with the `\\` command.

If there are several authors and their names are separated by the `\and` command, then the names
appear side by side. If, instead, we use `\\` the names are printed one below another. 

Thus

```Latex
\title{Title}
\author{Author 1\\
    Address line 11\\
    Address line 12\\
    Address line 13
    \and
    Author 2\\
    Address line 21\\
    Address line 22\\
    Address line 23}
\date{Month Date, Year}
```

produces [a big centered Title with two columns underneath (each one containing an author with 3
lines of address), and a date underneath (the date actually reads `Month Date, Year`)]

We may leave some of these arguments empty; for example, the command `\date{ }`
prints no date. **Note**, however, that if you simply omit the \date command itself, the
current date will be printed. 

The command `\thanks{this text will go inside a footnote}` can be given at any point within the
`\title`, `\author`, or `\date`. It puts a marker at this point and places the footnote text as a
footnote. (The general method of producing a footnote is to type `\footnote{footnote text}` at the
point we want to refer to.)

### Abstract

In the document classes `article` and `report`, an abstract of the document in special format can be
produced by the commands

```Latex
\begin{abstract}
  Abstract Text
\end{abstract}
```

In the `report` class this appears on the separate title page and in the `article` class it appears
below the title information on the first page (unless overridden by the title page option). This
command is not available in the `book` class.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Dividing the document

A book is usually divided into chapters, with chapters divided into sections, subsections, and so
on. LaTeX provides the following hierarchy of sectioning commands in the `book` and `report`
class. (Except for `\chapter` all these are available in `article` class also.)

```Latex
\chapter
\section
\subsection
\subsubsection
\paragraph
\subparagraph
```

Paragraphs and subparagraphs do not have numbers, and they have run-in headings. These sections can
actually have several paragraphs of text within them. (Subparagraphs have an additional
indentation.)


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
# References

[Indian TeX Users Group][tug_india], *LaTeX Tutorials: A Primer (2003 September)*

[tug_india]: http://www.tug.org.in
