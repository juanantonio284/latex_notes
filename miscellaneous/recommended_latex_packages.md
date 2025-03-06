# Recommended LaTeX packages

https://tex.stackexchange.com/questions/553/what-packages-do-people-load-by-default-in-latex

1

`microtype` It plays with ever-so-slightly shrinking and stretching of the fonts and with the extent to which text protrudes into the margins in a way that yields results that look better, that have fewer instances of hyphenation, and fewer overfull hboxes. It doesn't work with latex, you have to use pdflatex instead. It also works with lualatex and (protrusion only) with xelatex.

2

The family of AMS math packages. At least amsmath and amssymb. Also amsthm if I need theorems and the class I'm using doesn't already define them.

http://ctan.org/pkg/amsmath

3

I use `hyperref` for setting PDF metadata and to create links, both within the document and for clickable URLs. Even Elsevier has used urlbst to update their bibliography style to support URLs and DOIs; hyperref does the actual work of rendering url = and doi = BibTeX fields into clickable PDF links.

4

For citations and bibliographies, biblatex is the package of my choice. Key points:

    biblatex includes a wide variety of built-in citation/bibliography styles (numeric, alphabetic, author-year, author-title, verbose [full in-text-citations], with numerous variants for each one). A number of custom styles have been published.

    Modifications of the built-in or custom styles can be accomplished using LaTeX macros instead of having to resort to the BibTeX programming language.

    biblatex offers well-nigh every feature of other bibliography-related LaTeX packages (e.g. multiple/subdivided bibliographies, sorted/compressed citations, entry sets, ibidem functionality, back references). If a feature is not included, chances are high it is on the package authors' to-do list.

    The babel package is supported, and biblatex comes with localization files for about a dozen languages (with the list still growing).

    Although the current version of biblatex (2.8a) still allows to use BibTeX as a database backend, by default it cooperates with Biber which supports bibliographies using Unicode. Biber (currently at version 1.8) is included in TeX Live and MiKTeX. Many features introduced since biblatex 1.1 (e.g., advanced name disambiguation, smart crossref data inheritance, configurable sorting schemes, dynamic datasource modification) are "Biber only".


5

The todonotes package is a must have in all my documents.

The package enables you to insert small notes in the text marking things to do in the document. 

```LaTeX
\usepackage{todonotes}
\todo{Rewrite this answer \ldots}
\listoftodos % at any location in the document a list of the inserted notes can be generated
```

6

One package that’s really general purpose is nag: It doesn’t do anything, per se, it just warns when you accidentally use deprecated LaTeX constructs from l2tabu (English / French / German / Italian / Spanish documentation).

From the documentation:

    Old habits die hard. All the same, there are commands, classes and packages which are outdated and superseded. nag provides routines to warn the user about the use of those. As an example, we provide an extension that detects many of the “sins” described in l2tabu.

Therefore, I now always have the following in my header (before the \documentclass, thanks qbi):

\RequirePackage[l2tabu, orthodox]{nag}

It’s a bit like having use strict; in Perl: a useful best practice.
Share
Improve this answer
Follow
edited Apr 9, 2014 at 20:48
community wiki

7 revs, 5 users 61%
Konrad Rudolph

    24
    Somewhat better is \RequirePackage[l2tabu,orthodox]{nag} before \documentclass. The package docu also recommends this. – 
    qbi
    Commented Jul 29, 2010 at 18:40


