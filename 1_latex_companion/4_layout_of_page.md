# The Layout of the Page
<!-- Chapter 4 -->

In this chapter we will see how to specify different page layouts. Often a single document requires
several different page layouts. For instance, the layout of the first page of a chapter, which
carries the chapter title, is generally different from that of the other pages in that chapter.

1. Geometrical dimensions of the layout: an introduction to LaTeX's dimensional parameters for page
layout (ways to change them and visualize their values)

2. Changing the layout: an in-depth discussion of the packages `typearea` and `geometry`, both of
which provide sophisticated ways to implement page layout specifications

3. Dynamic page data: page numbers and marks: LaTeX concepts used to provide data for running
headers and footers

4. Page styles: formatting headers and footers (including many examples deploying the `fancyhdr`
package)

5. Visual formatting: commands that help in situations when the text does not fit into the layout
and manual intervention is required

6. Doing layout with class: a brief look at two generic classes that go a long way toward providing
almost full control over the page layout specification process


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Dynamic page data: page numbers and marks
<!-- 4.3 -->

LaTeX's **output routine**, which produces the typeset pages, works *asynchronously*. That is, LaTeX
assembles and prepares enough material to be sure that a page can be filled and then builds that
page, usually leaving some residual material behind to be used on the next page(s). Thus, while
preparing headings, paragraphs, and other page elements, it is usually not known on which page this
material will eventually be placed because LaTeX might eventually decide that this material will
not fit on the current page.[^this_problem]

When the final page is typeset, we might want to repeat some information from its contents in the
running header or footer (e.g. the current section head), to give the reader extra guidance.
Because LaTeX often reads too far ahead, a command might contain data that will actually not appear
on the final page; so you cannot save this information in commands when the material is collected.

LaTeX solves the problem of not being able to save this data in a command by providing a mark
mechanism through which you can identify data as being of interest for the assembled page. In the
output routine all marks from the page are collected and the first and the last mark are made
available. The detailed mechanism is explained in this section together with some useful extension
packages.

[^this_problem]: We have already discussed this problem in the section about page-wise footnote
numbering.

### LATEX page numbers
<!-- 4.3.1 -->

<!-- page 216 -->
The `\pagenumbering` command resets the `page` counter to 1 and redefines the command `\thepage`
to \style{page}. Ready-to-use page counter styles include: `Alph`, `alph`, `Roman`, `roman`, and
`arabic` (see Section A.1.4).

For example, an often seen convention is to number the pages in the front matter with `roman`
numerals and then to restart the page numbers using `arabic` numbers for the first chapter of the
main matter. You can manually achieve this effect by deploying the `\pagenumbering` command twice
(the `\frontmatter` and `\mainmatter` commands available with the `book` class implement this
set-up implicitly behind the scenes).

<!-- page 215 -->
The page number is controlled through a counter named `page`. 

* This counter is automatically stepped by LaTeX whenever it has finished a page—that is, *after* it
  has been used. Thus, it has to be initialized to 1 (whereas most other LaTeX counters require an
  initialization to 0 as they are stepped just before they get used). The command to access the
  typographical representation of the page number is `\thepage`

* Another subtle difference compared to other LaTeX counters: the `\thepage` command is not defined
  by the LaTeX kernel but instead comes into existence only after the first execution of a
  `\pagenumbering` declaration, which typically happens in the document class file.

Because of the asynchronous nature of the output routine you cannot safely use `\thepage` within the
document body. It is reliable only in declarations that influence the look and feel of the final
page built by the output routine. So the best way to access the page number for the current page in
the middle of the text is via a combination of the commands `\label` and `\pageref`.(These commands
should be put directly one following the other so that no page break can interfere.)

```latex
We are now on page~\label{p1}\pageref{p1}. This type of coding always gives correct results while
``page \thepage{}'', though okay at this point, will be wrong at a later point in the paragraph,
such as here: ``page \thepage'', because \LaTeX{} decided to break the paragraph over two pages.
```

The code above renders on two pages as

```
<!-- this is on actual page 6 -->
We are now on page 6. This type of coding always gives correct results while "page 6", though okay
<!-- this is on actual page 7 -->
at this point, will be wrong at a later point in the paragraph, such as here: "page 6", because
LaTeX decided to break the paragraph over two pages.
```

### lastpage—A way to reference it
<!-- 4.3.2 -->

Standard LaTeX has no way to refer to the number of pages in a document; that is, you cannot
write "this document consists of 6 pages" or generate "page 5 of 10" without manually counting the
pages yourself. The package lastpage by Jeffrey Goldberg sets out to overcome this problem by
automatically generating a label with the name LastPage on the last page, so that you can refer to
its page number via `\pageref{LastPage}`. Example 4-4-5 on page 226 demonstrates its use.

The string produced by that call to `\pageref` is the content of `\thepage` as it would appear on
the last page. If your document restarts page numbering midway through—for example, when the front
matter has its own numbering—this string will not reflect the absolute number of pages.

The package works by generating the label within the `\AtEndDocument` hook, making sure that any
pending floats are placed first. However, as this hook might also be used by other packages to place
textual material at the end of the document, there is a chance that the label may be placed too
early. In that case you can try to load `lastpage` after the package that generates this extra
material.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Visual formatting
<!-- 4.5 -->

The final stage of the production of an important document often needs some hand-formatting to avoid
bad page breaks. For this purpose, standard LaTeX offers the `\pagebreak` , `\nopagebreak`,
`\newpage`, and `\clearpage` commands.
<!-- [Book expounds on the obsolete \samepage declaration and alternatives.] -->
