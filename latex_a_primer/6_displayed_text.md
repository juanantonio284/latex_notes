# Tutorial VI: Displayed Text

There are many instances in a document when we want to visually separate a portion of text from its
surrounding material. One method of doing this is to typeset the distinguished text with added
indentation; this is called **displaying**. LaTeX has various constructs for displaying text
depending the nature of the displayed text.

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Quotations with the `quote` and `quotation` environments

If the quotation is several lines long, it is better to display it. 
By means of the commands `\begin{quote}` and `\end{quote}`, we give instructions to TeX to typeset
some material in a separate paragraph with additional indentation on either side.

Look at the following example of a quoted part with a **single** paragraph:

```Latex
Some mathematicians elevate the spirit of Mathematics to a kind of intellectual aesthetics. It
is best voiced by Bertrand Russell in the following lines.
\begin{quote}
    The true spirit of delight, the exaltation, the sense of being more than man, which is the
    touchstone of the highest excellence, is to be found in Mathematics as surely as in poetry ...
    Real life is, to most men, a long second best, a perpetual compromise between the ideal and the
    possible; but the world of pure reason knows no compromise, no practical limitations, no
    barriers to the creative activity embodying in splendid edifices the passionate aspiration
    after the perfect, from which all great work springs.
\end{quote}
Yes, to men like Russell, Mathematics is more of an art than science.
```

If the quotation runs into **several** paragraphs, we must use the `quotation` environment, by
enclosing the quotation within `\begin{quotation}` and `\end{quotation}`. As usual, paragraphs are
separated by blank lines while typing the source file.

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Poetry with the `verse` environment

```Latex
Contrary to popular belief, limericks are not always ribald. Some of them contain mathematical
concepts:
\begin{verse}
    A mathematician once confided\\
    That a M\"obius band is one sided\\
    You'll get quite a laugh\\
    If you cut it in half\\
    For it stays in one piece when divided
\end{verse}
There is an extension of this to Klein's bottle also.
```

* Line breaks are forced by the symbol `\\`
* Different stanzas are separated in the input by one (or more) blank lines
* If you do not want TeX to start a new page at a particular line break (if you want to keep rhyming
  couplets together in one page, for example), then use `\\*` instead of plain `\\`
* If you want more space between lines than what LaTeX deems fit, use `\\` with an optional length
  as in `\\[5pt]` which adds an extra vertical space of 5 points between the lines. (You can also
  type `\\*[5pt]` to keep couplets in one page.)


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Declarations

[From page 27 of *LaTeX: A Document Preparation System-User's Guide and Reference Manual*
(Second edition. ISBN 0-201-52983-1) by Leslie Lamport]

You may want to emphasize a large piece of text, such as a quotation. You can do this with the
`\emph` command, but that makes the input file hard to read because you have to search for the
closing right brace to see where the argument ends. Moreover, it's easy accidentally to delete the
closing brace when you edit the text. Instead, you can use the `\em` declaration, which tells LaTeX
to start emphasizing text (but you should use the `\emph` command for emphasizing small pieces of
text because it produces better spacing). In the following example, the `\end{quote}` tells TeX to
stop emphasizing text.

```Latex
This prose is very dull.
\begin{quote}
Wait!  \em Here is an exciting quote
\end{quote}
Aren't you glad all that excitement is over?
```

The command `\em` does not produce text; instead, it affects the way LaTeX prints text. Such a
command is called a declaration.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## Lists

### Bullets

The `itemize` environment gives us a bullet-list. For example it produces something like this:

```
One should keep the following in mind when using TeX

* TeX is a typesetting language and not a word processor
* TeX is a program and and not an application
* There is no meaning in comparing TeX to a word processor, since the design purposes are different
* TeX is the natural choice in one of these situations
    - If we want to typeset a document containing lot of Mathematics
    - If we want our typed document to look beautiful
    
Being a program, TeX offers a high degree of flexibility.
```

<!-- page 49 -->
The input which produces this is given below:

```Latex
One should keep the following in mind when using \TeX

\begin{itemize}
    \item \TeX\ is a typesetting language and not a word processor
    \item \TeX\ is a program and and not an application
    \item There is no meaning in comparing \TeX\ to a word processor, since the design purposes are
     different
    \item \TeX\ is the natural choice in one of these situations
        \begin{itemize}
            \item If we want to typeset a document containing lot of Mathematics
            \item If we want our typed document to look beautiful
        \end{itemize}
\end{itemize}
Being a program, \TeX\ offers a high degree of flexibility.
```

Note:

* The `\begin{itemize}`-`\end{itemize}` pair signifies we want a bullet-list of the enclosed
  material
* Each item of the list is specified by an `\item` command
* We can have lists within lists
* The command `\TeX\` is typed with a backslash after it

#### Levels of nesting

The `itemize` environment supports four levels of nesting, each with a different label (symbol) for
the items at each level:

```
• Bullets for the first level
    – Dashes for the second level
        ∗ Asterisk for the third level
            · Middle dot for the fourth level
```

Not satisfied with these default labels? You can try different symbols: 

```Latex
{
\renewcommand{\labelitemi}{$\triangleright$}
\begin{itemize}
    \item First item of a new list
    \item Second item
\end{itemize}
}
```

Note that the first level labels of the `itemize` environment are produced by the `\labelitemi`
command (read as "`label item i`"), which is an internal and invisible-to-the-user command.

The `\labelitemi` command is, by default, set as `\textbullet` to produce the default 'bullets'. In
the example above, by using `\renewcommand` we override the default with a choice of our own,
`$\triangleright$`, which produces the little triangles instead of bullets when rendering the
document. (To change the second, third, and fourth level labels change the `\labelitemii`,
`\labelitemiii`, and `\labelitemiv` commands, respectively.)

The **braces `{}` enclosing the whole code block above make the effect of the `\renewcommand`
local**. Meaning: this change of labels is only for this specific list; the next time we use an
itemize environment, the labels revert back to the original bullets. If we want the labels to be
changed in the entire document, then remove the braces.

For example:

Here the labels are chosen from the PostScript ZapfDingbats font[^note_package]. 

```Latex
{
\renewcommand{\labelitemi}{\ding{42}}
\renewcommand{\labelitemii}{\ding{43}}
\renewcommand{\labelitemiii}{\ding{44}}
\renewcommand{\labelitemiv}{\ding{45}}
\begin{itemize}
 \item The first item in the first level
 \item the second item in the first level
  \begin{itemize}
   \item The first item in the second level
   \item the second item in the second level
    \begin{itemize}
     \item The first item in the third level
     \item the second item in the third level
      \begin{itemize}
       \item The first item in the fourth level
       \item the second item in the fourth level
      \end{itemize}
    \end{itemize}
  \end{itemize}
\end{itemize}
}
```

[^note_package]: To access them, use the package `pifont` with the line `\usepackage{pifont}` in the document preamble.

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
### Ordered Lists
<!-- page 51 -->

A numbered list is produced by the `enumerate` environment in LaTeX:

```Latex
\begin{enumerate}
    \item prepare a source file with the extension "tex
    \item Compile it with \LaTeX to produce a "dvi" file
    \item Print the document using a "dvi" driver
\end{enumerate}
```

The `enumerate` environment supports four levels of nesting, each with a different label (symbol) 
for the items at each level:

```
1. The first item in the first level
2. the second item in the first level
    (a) The first item in the second level
    (b) the second item in the second level
        i. The first item in the third level
        ii. the second item in the third level
            A. The first item in the fourth level
            B. the second item in the fourth level
```

How about customizing the labels? 

Here there is an additional complication in that the labels for items in the same level must follow
a sequence (such as `1,2,3, ...` for the first level, `(a), (b), (c), ...` for the second and so
on). There is a method for doing it, but it will take us into somewhat deeper waters. Fortunately,
there is a package `enumerate` by David Carlisle, which makes it easy. 

Here is an example:

```
The three basic steps in producing a printed document using LaTeX are as follows:

Step 1. Prepare a source file with the extension tex
Step 2. Compile it with LaTeX to produce a dvi file
    i. Use a previewer (such as xdvi on X Window System) to view the output
    ii. Edit the source if needed
    iii. Recompile
Step 3. Print the document using a dvi driver (such as dvips)
```

```Latex
The three basic steps in producing a printed document using \LaTeX\ are as follows:

\begin{enumerate}[\hspace{0.5cm}Step 1.]
\item Prepare a source file with the extension "tex"
\item Compile it with \LaTeX to produce a "dvi" file
    \begin{enumerate}[i.]
    \item Use a previewer (such as "xdvi" on \textsf{X Window System}) to view the output
    \item Edit the source if needed
    \item Recompile
    \end{enumerate}
\item Print the document using a "dvi" driver (such as "dvips")
\end{enumerate}
```

As you can see, the labels `Step 1`, `Step 2`, and `Step 3` are produced by the optional argument 
`[\hspace{0.5cm}Step 1.]` immediately following the first `\begin{enumerate}` command.
(`\hspace{0.5cm}` provides an indentation at the left margin of the first level items, which the
enumerate environment does not produce by default. )

The labels `i`, `ii`, `iii` for the second level enumeration are produced by the optional 
`[i.]` following the second `\begin{enumerate}`. 


<!-- more details and examples of these customizations on page 53 -->

<!-- keep reading ... -->
<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- ## Descriptions and Definitions -->

<!-- There is a third type of list available off-the-shelf in LaTeX which is used in typesetting lists -->
<!-- like this:  -->

