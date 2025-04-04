# latex_notes

Personal notes on LaTeX

## 1_latex_companion

Notes from the book *The LaTEX Companion* (Second Edition. Fourth printing 2005. ISBN
0-201-36299-6) by Frank Mittelbach and Michel Goossens

* **1_intro.md** — an overview of the vast array of files used by a typical LaTeX system with its
    many components (talks about file extensions such as .tex, .bbl, .ps, .clo, .cls, .sty)

* **2_structure_of_latex_doc.md** — how the general principle of separation between layout and
    structure is implemented in LaTeX (This separation helps the user concentrate on content rather
    than having to worry about layout issues.) **Topics**: The structure of a source file,
    Sectioning commands, Combining several files

* **4_layout_of_page.md** — how to specify different page layouts. **Topics**: Geometrical
    dimensions of the layout, Changing the layout, Dynamic page data: page numbers and marks, Page
    styles, Visual formatting, Doing layout with class

* **4_layout_of_page.md** — This chapter gives an overview of the basic programming concepts
    underlying the LaTeX formatter. **Topics**: Linking markup and formatting, Page markup—Boxes
    and rules, Control structure extensions, Package and class file structure

<!-- * **.md** — -->
<!-- * **.md** — -->

## miscellaneous

* **latexmk_instructions.md** — simple notes to use the `latexmk` utility

* **listings_package_settings_reference.md** — settings to configure the `listings` package in LaTeX

* **markdown_to_latex_instructions.md** — instructions for using *Pandoc* to convert a text file
    with markdown syntax to latex syntax

* **recommended_latex_packages.md** — a subset of packages I found interesting from a list of
    recommended packages


## my_frontiers_article_template

* **my_class_1_frontiers_vanc.cls** — class file for a journal article

* **1_my_frontiers_template.tex** — sample file to show how the `.cls` file works


## lamport_latex_ref

Notes from the book *LaTeX: A Document Preparation System-User's Guide and Reference Manual*
(Second edition. ISBN 0-201-52983-1) by Leslie Lamport

* **sample2e.tex** — sample file that comes with an installation of LaTeX, here just for reference

* **abridged_sample2e.tex** — notes from the sample file, includes a little more content (from the
  textbook) and is easier to follow than the original
  
* **3** — notes from chapter 3 on *changing the type style* and the paragraph, basic math, and
    left-to-right(LR) *modes* in LaTeX
  
* **4_moving_info** — LaTeX often has to move information from one place to another. For example,
    the information contained in a table of contents comes from the sectioning commands that are
    scattered throughout the input file. Similarly, the command that generates a cross-reference to
    an equation must get the equation number from an equation environment which may occur several
    sections later. In other words, references appear in different places than the commands which
    create the information for those references ... **Topics**: Cross-References, Keys, Labels,
    Page References, Captions, Bibliography and Citation, Using BibTeX, Traditional Steps When
    Using BibTeX, Splitting Your Input, Making an Index or Glossary.
  
* **6_designing_it_yourself** — This chapter explains how to specify the visual appearance of a
    document. Commands specifying the visual appearance of the document are usually confined to the
    preamble, either as style declarations or in the definitions of commands and environments for
    specifying logical structures. **Topics**: Document and Page Style, Document-Class Options,
    Page Styles, Page Numbers, Configuring `headings` and `myheadings`, Title Page and Abstract,
    Line and Page Breaking, Numbering, Length, Spaces, and Boxes


## latex_a_primer

Notes from the book *LaTeX Tutorials: A Primer* (September 2003) by the 
[Indian TeX Users Group][tug_india]

* **1_simple_typesetting_and_fonts.md** — basic typesetting tricks and how fonts work

* **2_the_document.md** — overall appearance of the document, style for individual pages

* **5_toc-index-glossary.md** — creating a Table of Contents (and List of Figures, and List of
    Tables)[sections on Index and Glossary not summarized yet]

* **6_displayed_text.md** — distinguish text from other text, lists (bullets, numbers, letters)


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
[tug_india]: http://www.tug.org.in
