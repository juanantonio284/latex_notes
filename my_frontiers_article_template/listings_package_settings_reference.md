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