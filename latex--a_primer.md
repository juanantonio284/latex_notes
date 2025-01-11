<!-- tutorial 1 -->
# Simple Typesetting

## Spaces

In traditional typesetting, a little extra space is added to periods which end sentences and TEX
also follows this custom. But how does TEX know whether a period ends a sentence or not? It assumes
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

```
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

```
The numbers 1, 2, 3, etc.\ are called natural numbers. According to Kronecker, they were made by
God; all else being the works of Man.
```

### Space needed (after a command the following space is not inserted at all)

TEX gobbles up all spaces after a command. **Enter an escaped space `\ ` so that the compiler
focuses on that and not on the command.**

For example, to properly display the sentence: ```I think \LaTeX is fun```

you should write ```I think \LaTeX\ is fun```

<!-- ## Dashes -->
<!-- ## Accents -->
<!-- ## Special symbols -->
<!-- ## Text alignment -->

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
# Fonts

The actual letters and symbols (collectively called type) that LATEX (or any other typesetting
system) produces are characterized by their style and size. For example, in this book emphasized
text is given in italic style and the example inputs are given in typewriter style. We can also
produce smaller and bigger types. A set of types of a particular style and size is called a font.

## Type style

In LATEX, a type style is specified by family, series, and shape. Any type style in the output is a
combination of these three characteristics.

<!-- See table 1.1 on page 14 -->

### Commands vs. declarations

Each of these type style changing commands has an alternate form as a declaration.

A command is `\textbf{boldface}`, a declaration is `{\bfseries boldface}`. Declarations seem to end
in "shape", "series", or "family"—e.g. `upshape`, `mdseries`, `ttfamily`. (See table on page 15)

`\bfseries{triangle}` would not work (both the declaration and the text need to be in the braces).

## Type size

Traditionally, type size is measured in (printer) points. The default type that TEX produces is of
10 pt size. There are 10 **declarations** provided in LATEX for changing the type size:

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


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- tutorial 2 -->
# The Document

## \documentclass

In addition to specifying the type of document (which we must do, since LATEX has no default
document class), we can also specify some options which modify the overall appearance that the
document has by default. Thus the actual syntax of the `\documentclass` command is `\documentclass
[options]{class}`

Note that options are given in square brackets and not braces. (This is often the case with LATEX
commands—options are specified within square brackets, after which mandatory arguments are given
within braces.)

### Font size

We can select the size of the font for the normal text in the entire document with one of the
options 10pt 11pt 12pt. Thus we can say `\documentclass[11pt]{article}` to set the normal text in
our document to 11pt size. (The default is 10pt).

### Paper size

We know that LATEX has its own method of breaking lines to make paragraphs. It also has methods to
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

In LATEX parlance, each page has a "head" and "foot" usually containing such information as the
current page number or the current chapter or section. This is set by the command `\pagestyle{...}` 
where the mandatory argument can be any one of the following styles: `plain`, `empty`, `headings`,
`myheadings`.

The behavior pertaining to each of these is given below:

* `plain`: the page head is empty and the foot contains just the page number, centered with respect
  to the width of the text. (This is the default for the article class if no `\pagestyle` is
  specified in the preamble.)

* `empty`: both the head and foot are empty. In particular, no page numbers are printed.

* `headings`: this is the default for the book class. The foot is empty and the head contains the
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

<!-- continue at bottom of page 19 -->

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
# References

[Indian TEX Users Group][tug_india], *LATEX Tutorials: A Primer (2003 September)*

[tug_india]: http://www.tug.org.in
