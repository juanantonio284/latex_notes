# The Layout of the Page
<!-- Chapter 4 -->

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Dynamic page data: page numbers and marks
<!-- 4.3 -->

LaTEX’s output routine, which produces the typeset pages, works asynchronously. That is, LaTEX assembles and prepares enough material to be sure that a page can be ﬁlled and then builds that page, usually leaving some residual material behind to be used on the next page(s).

Thus, while preparing headings, paragraphs, and other page elements, it is usually not known on which page this material will eventually be placed because LaTEX might eventually decide that this material will not ﬁt on the current page. (We have already discussed this problem in the section about page-wise footnote numbering.) 

<!-- this is the problem: You cannot save this information in commands when the material is collected -->
When the ﬁnal page is typeset, we might want to repeat some information from its contents in the running header or footer (e.g. the current section head), to give the reader extra guidance. **You cannot** save this information in commands when the material is collected; during this phase LaTEX often reads too far ahead and your command would then contain data not appearing on the ﬁnal page.

LaTEX solves this problem by providing a mark mechanism through which you can iden- tify data as being of interest for the assembled page. In the output routine all marks from the page are collected and the ﬁrst and the last mark are made avail- able. The detailed mechanism is explained in this section together with some use- ful extension packages.

### LATEX page numbers
<!-- 4.3.1 -->

<!-- page 216 -->
The \pagenumbering command resets the `page` counter to 1 and redeﬁnes the command \thepage to \style{page}. Ready-to-use page counter styles include: `Alph`, `alph`, `Roman`, `roman`, and `arabic` (see Section A.1.4).

For example, an often seen convention is to number the pages in the front matter with `roman` numerals and then to restart the page numbers using `arabic` numbers for the ﬁrst chapter of the main matter. You can manually achieve this eﬀect by deploying the \pagenumbering command twice (the \frontmatter and \mainmatter commands available with the `book` class implement this set-up implicitly behind the scenes).

<!-- page 215 -->
The page number is controlled through a counter named `page`. 

* This counter is automatically stepped by LaTEX whenever it has ﬁnished a page—that is, *after* it has been used. Thus, it has to be initialized to 1 (whereas most other LaTEX counters require an initialization to 0 as they are stepped just before they get used). The command to access the typographical representation of the page number is \thepage

* Another subtle diﬀerence compared to other LaTEX counters: the \thepage command is not deﬁned by the LaTEX kernel but instead comes into existence only after the ﬁrst execution of a \pagenumbering declaration, which typically happens in the document class ﬁle.

Because of the asynchronous nature of the output routine you cannot safely use \thepage within the document body. It is reliable only in declarations that inﬂu- ence the look and feel of the ﬁnal page built by the output routine. So the best way to access the page number for the current page in the middle of the text is via a combination of the commands \label and \pageref. (These commands should be put directly one following the other so that no page break can interfere.)

```latex
We are now on page~\label{p1}\pageref{p1}. This type of coding always gives correct results
while ‘‘page \thepage{}’’, though okay at this point, will be wrong at a later point in the
paragraph, such as here: ‘‘page \thepage’’, because \LaTeX{} decided to break the paragraph over
two pages.
```

The code above renders on two pages as

```
<!-- this is on actual page 6 -->
We are now on page 6. This type of coding always gives correct results while ‘‘page 6’’, though okay
<!-- this is on actual page 7 -->
at this point, will be wrong at a later point in the paragraph, such as here: ‘‘page 6’’, because
LaTeX decided to break the paragraph over two pages.
```

### lastpage—A way to reference it
<!-- 4.3.2 -->

Standard LaTEX has no way to refer to the number of pages in a document; that is, you cannot write “this document consists of 6 pages” or generate “page 5 of 10” without manually counting the pages yourself. The package lastpage by Jeﬀrey Goldberg sets out to overcome this problem by automatically generating a label with the name LastPage on the last page, so that you can refer to its page number via \pageref{LastPage}. Example 4-4-5 on page 226 demonstrates its use.

The string produced by that call to \pageref is the content of \thepage as it would appear on the last page. If your document restarts page numbering midway through—for example, when the front matter has its own numbering—this string will not reﬂect the absolute number of pages.

The package works by generating the label within the \AtEndDocument hook, making sure that any pending ﬂoats are placed ﬁrst. However, as this hook might also be used by other packages to place textual material at the end of the docu- ment, there is a chance that the label may be placed too early. In that case you can try to load lastpage after the package that generates this extra material.

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Visual formatting
<!-- 4.5 -->

The ﬁnal stage of the production of an important document often needs some hand-formatting to avoid bad page breaks. For this purpose, standard LaTEX oﬀers the \pagebreak , \nopagebreak , \newpage , and \clearpage commands.
<!-- [Book expounds on the obsolete \samepage declaration and alternatives.] -->
