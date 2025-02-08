# Tutorial I: The Basics

## Simple Typesetting

### Spaces

In traditional typesetting, a little extra space is added to periods which end sentences and TeX
also follows this custom. But how does TeX know whether a period ends a sentence or not? It assumes
that every period not following an upper case letter ends a sentence[^logic_1].

[^logic_1]: The logic is: if it follows an upper case letter then it's likely an abbreviation and not
the end of a sentence.  

<!--  -->
#### Extra space after period needed (sentence ends with uppercase letter)

There are instances where a sentence ends in an upper case letter and you should manually **add an
extra space after the period with `\@`.**

For example, consider the following:

```
Carrots are good for your eyes, since they contain Vitamin A. Have you ever seen a rabbit
wearing glasses?
```
The right input to produce this is:

```Latex
Carrots are good for your eyes, since they contain Vitamin A\@. Have you ever seen a rabbit wearing
glasses?
```

#### Extra space after period not needed (period does not mark end a sentence)

There are instances where a period following a lowercase letter does not end a sentence. **Enter an
escaped space (\ ` `) so that the compiler focuses on the space and not on the period.** [Thus not
adding an extra space].

<!-- **Remove the extra space with a backslash and a space `\ `. (This is an escaped space.)** -->

For example:

```
The numbers 1, 2, 3, etc.  are called natural numbers. According to Kronecker, they were made
by God; all else being the work of Man.
```

To produce this (without extra space after etc.) the input should be

```Latex
The numbers 1, 2, 3, etc.\ are called natural numbers. According to Kronecker, they were made by
God; all else being the works of Man.
```

#### Space needed (after a command the following space is not inserted at all)

TeX gobbles up all spaces after a command. **Enter an escaped space \ ` ` so that the compiler
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
## Fonts

The actual letters and symbols (collectively called *type*) that LaTeX (or any other typesetting
system) produces are characterized by their *style* and *size*. For example, in this book
emphasized text is given in *italic style* and the example inputs are given in `typewriter style`.

A set of types of a particular style and size is called a *font*.

### Type style

In LaTeX, a *type style* is specified by a combination of *family*, *series*, and *shape*.

#### Styles

* **Families**: roman, sans serif, typewriter
    - commands: `\textrm{}`, `\textsf{}`, `\texttt{}`
    - declarations: `{\rmfamily loren ipsum ...}`, `{\sffamily loren ipsum ...}`, `{\ttfamily loren ipsum ...}`,
* **Series**: medium, boldface
    - commands: `\textmd{}`, `\textbf{}`
    - declarations: `{\mdseries loren ipsum ...}`, `{\bfseries loren ipsum ...}`
* **Shape**: upright, italic, slanted, small cap
    - commands: `\textup{}`, `\textit{}`, `\textsl{}`, `\textsc{}`
    - declarations: `{\upshape loren ipsum ...}`, `{\itshape loren ipsum ...}`, `{\slshape loren ipsum ...}`, 
      ` {\scshape loren ipsum ...}`

**By default** we get **roman family, medium series, upright shape** type style in a LaTeX output.
  Thus, for instance:

* the `\textit` command produces roman family, medium series, italic shape type
* the `\textbf` command produces roman family, boldface series, upright shape type

We can combine these commands to produce a wide variety of type styles. For example:

```latex
\textsf{\textbf{this text is sans serif family, boldface series, upright shape}} # the upright is default
\textrm{\textsl{roman family, medium series, slanted shape}} # the medium is default
```

**Note: commands vs. declarations**

Each of these type style changing commands has an alternate form as a declaration. A command is
`\textbf{boldface}`, a declaration is `{\bfseries boldface}`. Thus `\bfseries{triangle}` would not
work (both the declaration and the text need to be in the braces).

(Notice that declarations seem to end in the words 'shape', 'series', or 'family'—e.g. `upshape`,
`mdseries`, `ttfamily`.) 

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
### Type size

Traditionally, type size is measured in (printer) points. The default type that TeX produces is of
10 pt size. 

There are 10 **declarations** provided in LaTeX for changing the type size:

```latex
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
sequence with `\tiny` producing the smallest and `\Huge` producing the largest. **Note** that these
are only in declaration form, there are no commands.
