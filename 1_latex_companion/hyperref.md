# hyperref—Active references
<!-- Mostly from Goossens section 2.4 Managing references, this subsection is 2.4.5 -->

The `hyperref` package makes it possible to turn all cross-references (citations, table of contents,
and so on) into hypertext links. It works by extending LaTeX cross-referencing commands
(including the table of contents, bibliographies, and so on) to produce `\special` commands that a
dvi driver or pdfTeX can turn into hypertext links. `hyperref` also provides new commands to allow
the user to write ad hoc hypertext links, including those to external documents and URLs. The
package is described in detail elsewhere[^elsewhere] and in its own manual.

The usage of `hyperref` can be quite easy. Just including it in your list of loaded packages (as the
last package) suffices to turn all cross-references in your document into hypertext links. 

The most important options in the package are

* `colorlinks`, which makes the text of the link come out in color instead of with a box around it,
  and 
* `backref`, which inserts links in the bibliography pointing to the place where an entry was cited. 

The package offers a number of ways to inﬂuence the behavior of the PDF file produced from your
document as well as ways to inﬂuence the behavior of the PDF viewer, such as the Adobe Reader.

`hyperref` is compatible with the natbib package and the listings package, among others. 

[^elsewhere]: Reference # 56, pages 35–67: Goossens and Rahtz. *The LaTeX Web Companion: Integrating
TeX, HTML, and XML*. This book teaches (scientific) authors how to publish on the web or other
hypertext presentation systems. The book explains how to make full use of the Adobe Acrobat format
from LaTeX, convert legacy documents to HTML or XML, make use of math in web applications, use
LaTeX as a tool in preparing web pages, read and write simple XML/SGML, and produce high-quality
printed pages from web-hosted XML or HTML pages using TeX or PDF.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->

https://www.overleaf.com/learn/latex/Hyperlinks

One must be careful when importing hyperref: usually, it has to be the last package to be imported—but there might be some exceptions to this rule. 

<!-- from official reference -->

## Package options

[The hyperref manual is not designed very well, it makes it seem as if page 10 contains all the
options; but those the options listed on page 10 are only those that are procesed as the package is
read. Really you need to look at all of chapter 5 and beyond. Section 5.10 contains a big
alphabetical list (a complete listing of available options for hyperref, arranged
alphabetically).]

All user-configurable aspects of hyperref are set using a single ‘key=value’ scheme (using the `keyval` package) with the key `Hyp`. The options can be set either in the optional argument to the `\usepackage` command, or using the `\hypersetup` macro. 

When the package is loaded, a file `hyperref.cfg` is read if it can be found, and this is a convenient place to set options on a site-wide basis. 

Note however that some options (for example unicode) can only be used as package options, and not in `\hypersetup` as the option settings are processed as the package is read. 

These options should be set after the package is loaded; otherwise LATEX expands their values prematurely. Also LATEX strips spaces in options. Especially option ‘pdfborder’ requires some care. Curly braces protect the value, if given as package option. They are not necessary in \hypersetup.



### Example

```latex


```

* `pdfusetitle`: If option pdfusetitle is set then hyperref tries to derive the values for pdftitle and pdfauthor from \title and \author. An optional argument for \title and \author is supported (class amsart).

* `pdfpagemode`: determines how the file is opening in Acrobat; the possibilities are `UseNone`, `UseThumbs` (show thumbnails), `UseOutlines` (show book- marks), `FullScreen`, `UseOC` (PDF 1.5), and `UseAttachments` (PDF 1.6). If no mode if explicitly chosen, but the bookmarks option is set, UseOutlines is used


<!-- not sure this worked -->
<!-- * `pdfpagelabels`: Page labels are essentially a way to assign user-friendly names or numbers to pages or page ranges in a PDF document. -->


<!-- forum question -->
<!-- https://latex.org/forum/viewtopic.php?t=1135 -->

<!-- official reference -->
https://ctan.math.illinois.edu/macros/latex/contrib/hyperref/doc/hyperref-doc.html

