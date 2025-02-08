# Tutorial II: The Document

## 1. Modify overall appearance of document with `\documentclass`

In addition to specifying the type of document (which we *must* do, since LaTeX has no default
document class), we can also specify some options which modify the overall appearance that the
document has by default. 
Thus the actual syntax of the `\documentclass` command is `\documentclass[options]{class}`

Note that options are specified within square brackets, after which mandatory arguments are given
within braces. (This is often the case with LaTeX commands.)

### Font size

We can select the size of the font for the normal text in the entire document with one of the
options `10pt`, `11pt`, or `12pt`. Thus we can say `\documentclass[11pt]{article}` to set the
normal text in our document to `11pt` size. (The default is `10pt`).

### Paper size

We know that LaTeX has its own method of breaking lines to make paragraphs. It also has methods to
make vertical breaks to produce different pages of output. For these breaks to work properly, it
must know the width and height of the paper used. 

The various options for selecting the paper size are given below. Normally, the longer dimension is
the vertical one, i.e. the height of the page. The default is `letterpaper`.

|    **command**   |   **size**   |
|:----------------:|:------------:|
|   `letterpaper`  |   11×8.5 in  |
|   `legalpaper`   |   14×8.5 in  |
| `executivepaper` | 10.5×7.25 in |
|     `a4paper`    |  20.7×21 in  |
|     `a5paper`    |  21×14.8 in  |
|     `b5paper`    |  25×17.6 in  |

### Page formats

**Columns**

There are options for setting the contents of each page in a single column (as is usual) or in two
columns (as seen in articles or dictionaries). The options are `onecolumn` and `twocolumn`
(the default is `onecolumn`).

There are also options to specify whether the document will be finally printed on one or both sides
of each paper. The options are `oneside` and `twoside`. 

**Sides**

One of the differences is that with the `twoside` option, page numbers are printed on the right on
odd-numbered pages and on the left on even numbered pages, so that when these printed back to back,
the numbers are always on the outside, for better visibility. The default is `oneside` for the
classes `article`, `report`, and `letter` and `twoside` for the `book` class.

**Chapter opening**

In the `report` and `book` classes chapters always begin on a new page, leaving blank space in the
previous page, if necessary. 

In the `book` class there is the additional restriction that chapters begin only on odd-numbered
pages, leaving an entire page blank, if need be. Such behavior is controlled by the options
`openany` and `openright`.

The default is `openany` for the `report` class (so that chapters begin on "any" *new* page) and
`openright` for the `book` class (so that chapters begin only on *new* right, i.e. an odd numbered
page).

**Title**

There is also a provision in LaTeX for formatting the "title" (the name of the document, authors,
etc.) of a document with special typographic consideration. 

* In the `article` class, the *title* is printed along with the text following on the first page

* For the `report` and `book` classes, the *title* is printed on a separate title page

* This is controlled by the options `notitlepage` (default for `article`) and `titlepage`
  (default for `report` and `book`)[^note_1]

[^note_1]: As with the other options, the default behavior can be overruled by explicitly specifying
an option with the `documentclass` command.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## 2. Set the style for individual pages with `\pagestyle`

In LaTeX parlance, each page has a "head" and "foot" usually containing such information as the
current page number or the current chapter or section. With the `\pagestyle{...}` command
(with mandatory arguments `plain`, `empty`, `headings`, or `myheadings`) we can set the style for
the individual pages. 

The behavior pertaining to each of these is given below:

* `plain`: the page head is empty and the foot contains just the page number, centered with respect
  to the width of the text. (This is the default for the `article` class if no `\pagestyle` is
  specified in the preamble.)

* `empty`: both the head and foot are empty (no page numbers are printed)

* `headings`: The foot is empty and the head contains the page number and names of the chapter
  section or subsection, depending on the document class and its options as given below. (This is
  the default for the `book` class.)
  
    |   **Class**  | **Option** | **Left Page** | **Right Page** |
    |:------------:|:----------:|:-------------:|:--------------:|
    | book, report |  one-sided |       —       |     chapter    |
    | book, report |  two-sided |    chapter    |     section    |
    |    article   |  one-sided |       —       |     section    |
    |    article   |  two-sided |    section    |   subsection   |


* `myheadings` the same as *headings*, except that the 'section' information in the head is not
  predetermined, but to be given explicitly using the commands `\markright` or `\markboth`

To customize the style for **only** the current page, use `\thispagestyle{style}` (where *style* is
the name of one of the styles above). For example, the page number may be suppressed for the
current page alone by the command `\thispagestyle{empty}`. (Note that only the *printing* of the
page number is suppressed, not the counting—i.e. the next page will still be numbered with the next
number in the sequence.)

<!-- skipped II.2.1. Heading declarations -->

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## 3. Set `\pagenumbering`

The style of page numbers can be specified by the command `\pagenumbering{...}` The possible
arguments to this command and the resulting style of the numbers are given below:

* `arabic`: Indo-Arabic numerals
* `roman`: lowercase Roman numerals
* `Roman`: upper case Roman numerals
* `alph`: lowercase English letters
* `Alph`: uppercase English letters

The default value is `arabic`. This command resets the page counter. 

Thus for example, to number all the pages in the 'Preface' with lowercase Roman numerals and the
rest of the document with Indo-Arabic numerals, declare `\pagenumbering{roman}` at the beginning of
the preface and issue the command `\pagestyle{arabic}` immediately after the first `\chapter`
command. We can make the pages start with any number we want by the command `\setcounter{page}
{number}` where number is the page number we wish the current page to have.

## 4. `\setlength`

Each page that LaTeX produces consists not only of a head and foot as discussed above but also a
body containing the actual text. In formatting a page, LaTeX uses the width and heights of these
parts of the page and various other lengths such as the left and right margins. The values of these
lengths are set by the paper size options and the page format and style commands. These values can
be changed with the command `\setlength`. For example, `\setlength{\textwidth}{15cm}` makes the
width of text 15 cm. 

The package `geometry` gives easier interfaces to customize page format.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Parts of a document

Documents (especially longer ones) are divided into chapters, sections, and so on. There may be a
title *part* (which may be on a separate title *page*) and an abstract. All these require special
typographic considerations and LaTeX has a number of features which automate this task.

### Title

The "title" is printed in a separate page for the document classes `book` and `report` and in the
first page of the document for the class `article`. (Recall that this behavior can be modified by
the options `titlepage` or `notitlepage`.)

To produce a title, we make use of the commands: 

```Latex
\title{document name}
\author{author names}
\date{date text}
\maketitle % must issue this command to actually typeset the title
```

By default, all entries produced by these commands are centered on the lines in which they appear.
If a title text is too long to fit in one line it will be broken automatically, but we can choose
the break points with the `\\` command.

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

produces a big centered Title, two columns underneath (each one containing an author with 3 lines of
address), and a date underneath (this actually reads `Month Date, Year`).

**Note** that if you simply omit the `\date` command, the current date will still be printed. To
  avoid printing a date insert the command `\date{ }`, i.e. the command with blank arguments.

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

Each sectioning command also has a "starred" version which does not produce numbers; thus 
`\section*{name}` has the same effect as `\section{name}`, but produces no number for this section.
  
Paragraphs and subparagraphs do not have numbers, and they have run-in headings. These sections can
actually have several paragraphs of text within them. (Subparagraphs have an additional
indentation.)

You may have noted that LATEX has a specific format for typesetting the section headings, such as
the font used, the positioning, the vertical space before and after the heading and so on. All
these can be customized, but it requires some TEXpertise and cannot be addressed at this point.
However, the package `sectsty` provided some easy interfaces for tweaking some of these settings.

### More on sectioning commands

#### In the `book` and the `report` classes:

* the `\chapter` command shifts to the beginning of a new page and prints the word 'Chapter', a
  number, and—beneath it—the name of the chapter passed as the argument of the command. Example:
  `Chapter I Name of Chapter`

* the `\section` command produces two numbers(separated by a dot) indicating the chapter number and
  the section number followed by the name we have given. It does not produce any text
  like 'Section'. Example: `I.I Name of Section`

* subsections have three numbers indicating the chapter, section and subsection

* subsubsections and commands below it in the hierarchy do not have any numbers

* some books and longish documents are divided into parts also. LATEX also has a `\part` command for
  such documents. In such cases, `\part` is the highest in the hierarchy, but it does not affect
  the numbering of the lesser sectioning commands

#### In the `article` class:

* `\section` is highest in the hierarchy and produces single number like `\chapter` in book.(It does
  not produce any text like 'Section') 

* subsubsections also have numbers, but none below have numbers
