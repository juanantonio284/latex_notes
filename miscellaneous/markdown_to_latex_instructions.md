# Using Pandoc to convert a file's format

## TLDR

```Bash

cd path/to/directory

pandoc --columns=100 -f markdown-auto_identifiers -t latex input_file.md > output_file.tex
# --columns=100: columns are 100 characters wide (this setting affects wrap and other things)
# -f: from 
# -t: to  
# markdown-auto_identifiers: avoids having all sections wrapped with the \hypertarget directive 
#                            (which happens when just using the "markdown" option)
#                            see more here https://github.com/jgm/pandoc/issues/8744

pandoc --listings --columns=100 -f markdown-auto_identifiers -t latex input_file.md > output_file.tex
# same as above but uses the listings package from latex, which means that:
#   - code blocks use \begin{listings} instead of \verbatim
#   - `inline` markdown uses \passthrough and other code instead of \textttt

```

## Further

* [Pandoc manual][]

* [`\hypertarget` issue][issue_8744]

* [tightlist][]

* [passthrough][]

[Pandoc manual]: https://pandoc.org/MANUAL.html#defaults-files
[issue_8744]: https://github.com/jgm/pandoc/issues/8744
[tightlist]: https://github.com/ozanmakes/markup.rocks/issues/4
[passthrough]: https://github.com/jgm/pandoc/issues/5696
