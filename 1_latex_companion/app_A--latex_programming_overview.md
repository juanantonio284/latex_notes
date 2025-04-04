# Appendix A: A LaTeX Overview for Preamble, Package, and Class Writers

This chapter gives an overview of the basic programming concepts underlying the LaTeX formatter.

1. Linking markup and formatting: how to define new commands and environments, including those with
an optional argument
    
    * counters and their representation
    * horizontal and vertical space parameters and how they are handled

2. Page markup—Boxes and rules: TeX/LaTeX boxes and their use (a good understanding of this topic is
very important to fully appreciate and exploit the information presented)

3. Control structure extensions: two package files, `calc` and `ifthen`, to make calculations and
building control structures with LaTeX easier

4. Package and class file structure: a detailed description of the LaTeX2ε interface that allows you
to define your own options for packages and class files.


<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
## A.1 Linking markup and formatting

This section reviews the syntax for defining commands and environments with LaTeX. It is important
that you exclusively use the LaTeX constructs described below, rather than the lower-level TeX
commands. Then, not only will you be able to take advantage of LaTeX's consistency checking, but
your commands will also be portable, (probably) without modification, to future versions of LaTeX.

### A.1.1 Command and environment names

**Commands**

In the current LaTeX incarnation, it is possible to enter accented characters and other non-ASCII
symbols directly into the source, so it would seem reasonable to expect that such characters could
also be used in command and environment names (e.g. `\größer`). However, this is not the case—LaTeX
multi-character command names must be built from basic ASCII letters (i.e. `a-z` and `A-Z`). This
means that `\vspace*` is actually not a command by itself; rather, it is the command `\vspace`
followed by the modifier `*`. Technically, you could write `\vspace *`(as the space is ignored) or
even put the `*` on the next line of your document [although this is bad style].

**Environments**

On the other hand, names of environments are different. In this case the `*` is part of the name and
spaces preceding it are not ignored. Thus, when writing `\begin{figure *}`, the space would become
part of the name and is not recognized as the start of a `figure*` environment. But it is best to
rely on officially supported names—those containing only lowercase and uppercase letters and the
star character.

**Citation and label keys**

Strictly speaking, `\cite` and `\label` keys have the same kind of restriction. Nevertheless, it has
become common practice to use keys containing colons (e.g. `ec:cmds`), so that most packages
provide extra support to allow for at least the colon character in such keys. 

Characters outside the ASCII range and characters used in LaTeX's syntax (e.g. `_` or `#`) can never
be used in names, whether they are keys, counters, environments, or multi-character command names.

With single-character command names, the situation is different again: any(single) character can be
used. For example, `\$` is a perfectly valid LaTeX command; but `\foo$bar` would be interpreted as
the command `\foo` followed by the start of a math formula (signaled by `$`) followed by the
(math) characters `b`, `a`, and `r`, and any following text will also be typeset in math mode.

LaTeX commands (i.e. those constructs starting with a backslash) are classified into three basic
categories: 

1. document-level commands
2. package and class writer commands
3. internal "kernel" commands

**Document-level commands**

Document-level commands, such as `\section `, `\emph` , and `\sum` , usually have (reasonably) short
names, all in lowercase.

**Class and package writer commands**

Class and package writer commands, by convention, have longer mixed-case names, such as
`\InputIfFileExists` and `\RequirePackage`. Some of them can be usefully applied in the document
source, but many will stop working after `\begin{document}` has been processed.

**Internal LaTeX commands**

Most of the internal commands used in the LaTeX implementation, such as `\@tempcnta`,
`\@ifnextchar`, and `\z@` contain `@` in their name. This effectively prevents these names from
being used in documents for user-defined commands. However, it also means that they cannot appear
in a document, even in the preamble, without taking special precautions.

**Careful with internal commands**

As a few of the examples in this book demonstrate, it is sometimes necessary to have such bits
of "internal code" in the preamble. The commands `\makeatletter` and `\makeatother` make this easy
to do; the difficult bit is to remember to add them, failure to do so can result in some strange
errors. For an example of their use, see page 852. Note that package and class files should never
contain these commands: `\makeatletter` is not needed as this is always set up when reading such
files; and the use of `\makeatother` would prematurely stop this behavior, causing all kinds of
havoc.

Unfortunately, for historical reasons the distinction between these categories is often blurred. For
example, `\hbox` is an internal command that should preferably be used only in the LaTeX kernel,
whereas `\m@ne` is the constant `-1` and could have been `\MinusOne`. Nevertheless, this rule of
thumb is still useful: if a command has `@` in its name, then it is not part of the supported LaTeX
language—and its behavior may change in future releases! Any such command should be used with great
care. On the other hand, mixed-case commands or those described in the LATEX Manual^
[latex_manual] are guaranteed to be supported in future releases of LaTeX2ε.

[^latex_manual]: Leslie Lamport. LaTeX: A Document Preparation System: User's Guide and Reference
Manual. Addison-Wesley, Reading, MA, USA, 2nd edition, 1994. ISBN 0-201-52983-1. Reprinted with
corrections in 1996. The ultimate reference for basic user-level LATEX by the creator of LATEX
2.09. It complements the material presented in this book.

<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
### A.1.4 Defining and changing counters
<!-- pdf 872, book 851 -->

Every number internally generated by LaTeX has a **counter** (register) associated with it. The name of the counter is usually identical to the name of the environment or the command that generates the number except that it does not start with `\`. 

**Counters used in LaTeX's standard document classes**

```
part            paragraph       figure        enumi
chapter         subparagraph    table         enumii
section         page            footnote      enumiii
subsection      equation        mpfootnote    enumiv
subsubsection
```

An environment declared by `\newtheorem` can also have a counter associated with it---this counter
will also have the same name as that of the environment---unless the optional argument indicates
that it is to be numbered together with another environment.

The value of a counter is a single integer. Several counters can be combined into a number, as is
usually the case for numbering section headings. For example, in the book or report classes,
`7.4.5` identifies the fifth subsection of the fourth section in the seventh chapter.

#### Basic LaTeX commands to define counters and modify/display counter values[^counter_commands] 

[^counter_commands]: These commands are much more powerful if used in conjunction with the calc
package, which is discussed in Section A.3.1.


1. `\newcounter{newctr}[oldctr]`
2. `\@addtoreset{reset-ctr}{ctr}` and `\@removefromreset{reset-ctr}{ctr}`
3. `\setcounter{ctr}{val}` and `\addtocounter{ctr}{val}`
4. `\stepcounter{ctr}` and `\refstepcounter{ctr}`


##### 1. `\newcounter{newctr}[oldctr]`

This command globally defines a new counter, `newctr`, and initializes it to zero. If a counter with
the name `newctr` is already defined, an error message is printed. When you specify the name of
another counter as the optional argument, `oldctr`, then the newly defined `newctr` is reset when
the counter `oldctr` is incremented with the `\stepcounter` or `\refstepcounter` command. It also
defines the command `\thenewctr` to expand to `\arabic{newctr}`.

##### 2. `\@addtoreset{reset-ctr}{ctr}` and `\@removefromreset{reset-ctr}{ctr}`

The operation that defines that one counter is reset whenever another counter is stepped is also available as the kernel command `\@addtoreset`. Unfortunately, the opposite declaration is not available in the kernel, but only when loading the package `remreset`. If this small package is loaded, then counters can be unraveled if necessary. For example, the `report` class defines that the footnote counter is to be reset whenever a new chapter starts.

If you want your footnotes nevertheless to be numbered sequentially throughout a document, then
specifying 

```latex
\usepackage{remreset} 
\makeatletter \@removefromreset{footnote}{chapter} \makeatother
```
in the preamble, or the equivalent code in a package or class, will do the job.

##### 3. `\setcounter{ctr}{val}` and `\addtocounter{ctr}{val}`

With `\setcounter` the value of counter `ctr` is globally set equal to the value `val`.
With `\addtocounter` it is globally incremented by `val`.


##### 4. `\stepcounter{ctr}` and `\refstepcounter{ctr}`

Both commands globally increment the counter `ctr` and reset all subsidiary counters---that is,
those declared with the optional argument `oldctr` on the \newcounter command or with the first
argument of `\@addtoreset`.

The `\refstepcounter` command additionally defines the current `\ref` value to be the text generated
by the command `\thectr`. Note that whereas stepping a counter is a global operation, setting the
current `\ref` value is done locally and thus is only valid inside the current group.

As a result the next example does not produce the desired result but instead picks up the section
number. The correct solution would be to move \refstepcounter before the `\textbf` command.




<!-- ≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈***≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈≈ -->
<!-- ## A.2 Page markup—Boxes and rules -->
<!-- ## A.3 Control structure extensions -->
<!-- ## A.4 Package and class file structure --> <!-- pdf 906 -->