# Setting up the `listings` package in LaTeX

## Sample Code

```LaTeX

%% -------------------------------------------------------------------------------------------------
%%    Setting up the listings package
%% -------------------------------------------------------------------------------------------------
% This package serves to display text, specifically to create boxes with code in them
% https://www.overleaf.com/learn/latex/Code_listing

\RequirePackage{listings} % Typeset source code listings

% general settings ...................................................
% These settings apply both when you use the plain \begin{lstlisting} ... construction, and also
% when using a specific styles (if the style definition has not overridden one of the definitions
% here)
\lstset{
  backgroundcolor=\color{lime!10},    % background color (requires color or xcolor package)
  commentstyle=\color{blue!30!black}, % comment style
  basicstyle=\ttfamily\small,         % font family\size (instead of small can try footnotesize)
  keywordstyle=\color{red!75!black},  % keyword style  
  stringstyle=\color{green!40!black}, % style of strings in source language
  frame=single,                       % show a frame surrounding code (see more at note i)
  % numbers=left,                       % Add line numbers on the left side
  % numberstyle=\tiny,                  % style used for line-numbers
  % numbersep=5pt,                      % distance of line-numbers from the code
  } 

% [style=numbers] ....................................................
% These settings apply when you use \begin{lstlisting}[style=numbers] ... \end{lstlisting}
\lstdefinestyle{numbers}
    {
    backgroundcolor=\color{cyan!10}, 
    % frame=none, % notice how this overrides the setting in lstset
    numbers=left, 
    numberstyle=\tiny, 
    numbersep=5pt                 
    } 

% [style=fitmore] ....................................................
\lstdefinestyle{fitmore}
    {
    % backgroundcolor=\color{orange!10},
    basicstyle=\ttfamily\footnotesize,
    % breakatwhitespace=true, % did not work as expected
    breaklines=true
    }

```

## More settings

```LaTeX
\lstset{
  backgroundcolor=\color{gray!10},    % background color (requires color or xcolor package)
  commentstyle=\color{blue!30!black}, % comment style
  basicstyle=\ttfamily\small,         % font size/family/etc (e.g. basicstyle=\ttfamily\small)
  keywordstyle=\color{red!75!black},  % keyword style  
  stringstyle=\color{green!40!black}, % style of strings in source language
  frame=single,                       % show a frame surrounding code (see more at note i)
  % numbers=left,                       % Add line numbers on the left side
  % numberstyle=\tiny,                  % style used for line-numbers
  % numbersep=5pt,                      % distance of line-numbers from the code
  % note sure about these ones ...................  
  % keepspaces=true,                    % ii  
  % breakatwhitespace=true,             % if true, it allows line breaks only at white space
  % breaklines=true,                    % true activates automatic line breaking of long lines
  % showspaces=true,                    % lets all blank spaces appear or as blank spaces
  % showstringspaces=true,              % lets blank spaces in strings appear or as blank spaces
  % showtabs=true,                      % make tabulators visible or invisible. If you choose 
                                        % invisible tabulators but visible spaces, tabulators are 
                                        % converted to an appropriate number of spaces.
  % have not tried ...............................
  % tabsize,                            % default tabsize
  % escapeinside,                       % specify characters to escape from source code to LaTeX 
  % captionpos,                         % position of caption (t/b)
  % prebreak,                           % displaying mark on the end of breaking line
  % problematic ..................................
  % rulecolor=\color{blue},             % iii 
}

% i: none/leftline/topline/bottomline/lines/single/shadowbox
%    draws either no frame, a single line on the left, at the top, at the bottom, at the top and
%    bottom, a whole single frame, or a shadowbox. Note that fancyvrb supports the same frame types
%    except shadowbox. The shadow color is rulesepcolor (see reference manual)

% ii: true tells the package not to drop spaces to fix column alignment and always converts
%     tabulators to spaces. (It's supposed to help keep indentation? I don't really notice a
%     difference.)

% iii: supposed to specify the colour of the frame-box, breaks the compilation

```

## Further

* https://www.overleaf.com/learn/latex/Code_listing
* https://www.overleaf.com/learn/latex/Using_colors_in_LaTeX
