# Writing scientific papers in LaTex (Tips and Tricks)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- param::isNotitle::true:: -->

- [TeX Engine Settings](#tex-engine-settings)
- [Aesthetics](#aesthetics)
  - [Balancing Columns on the Last Page in a Two-Column Document](#balancing-columns-on-the-last-page-in-a-two-column-document)
  - [Highlighting](#highlighting)
    - [Round label](#round-label)
    - [Grey highlight](#grey-highlight)
- [Meta](#meta)
  - [Finding weird Unicode](#finding-weird-unicode)
  - [Highlight updates or inline comments](#highlight-updates-or-inline-comments)
- [Math](#math)
- [Glossaries](#glossaries)
- [Bibliography](#bibliography)
  - [Clean bib files](#clean-bib-files)
  - [Use Biblatex](#use-biblatex)
- [Tables](#tables)
  - [Hide columns](#hide-columns)
- [SI-units](#si-units)
- [Clever reference](#clever-reference)
- [Figures](#figures)
  - [ETH Figure Tool](#eth-figure-tool)
  - [Python to Tikz](#python-to-tikz)
  - [Extract data from existing figures](#extract-data-from-existing-figures)
  - [Indicate lines in a plot](#indicate-lines-in-a-plot)
- [Preparing for submission](#preparing-for-submission)
  - [Clean-up Project](#clean-up-project)
    - [LaTeX cleaner's main features:](#latex-cleaners-main-features)
  - [Shortening a Paper](#shortening-a-paper)
  - [Reducing space after caption](#reducing-space-after-caption)
    - [Biblatex hacks](#biblatex-hacks)
- [Updating manuscript](#updating-manuscript)
  - [Change color of single reference using biblatex](#change-color-of-single-reference-using-biblatex)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## TeX Engine Settings

Settings in VSCode with increased memory size (pgfplots) and shell escape:
```json
{
			"name": "lualatexmk",
			"command": "latexmk",
			"args": [
                "-shell-escape",                // <---- added this line
                "--extra-mem-bot=10000000",     // <---- added this line
                "--extra-mem-top=10000000",     // <---- added this line
				"-synctex=1",
				"-interaction=nonstopmode",
				"-file-line-error",
				"-lualatex",
				"-outdir=%OUTDIR%",
				"%DOC%"
			],
			"env": {}
		}
```

## Aesthetics

### Balancing Columns on the Last Page in a Two-Column Document

In LaTeX, when using a two-column format, the last page may sometimes have only one full column, leaving an unbalanced layout. To ensure both columns are evenly distributed, use the `balance` package. Adding `\balance` before the last content forces LaTeX to split the text evenly across both columns. This results in a cleaner and more professional layout, avoiding a single long column with excessive white space. If fine-tuning is needed, manual adjustments with `\vfill` and `\newpage` can be used. Example:

```latex
\usepackage{balance}  % Include in the preamble
\balance  % Place before the last content
```

### Highlighting

#### Round label

```latex
\usepackage{tikz}
\usepgfplotslibrary{external}

\definecolor{mycolor}{RGB}{112,45,128}
\newcommand{\roundlabel}[1]{\tikzexternaldisable \tikz[baseline=(char.base)]{
            \node[rectangle, rounded corners=0.65mm,inner sep=0.65mm,fill=mycolor, draw=mycolor, text=white, font=\itshape](char) {#1};}\tikzexternalenable}
```

Example usgae: `\roundlabel{Message 5/Conclusion:}`

![image](https://github.com/DRAMCO/writing-scientific-papers-in-latex-tips-and-tricks/assets/8626571/eec84614-0f77-400a-a512-d664b24c884f)



#### Grey highlight

```latex
\newcommand{\syntaxHighlight}[1]{\colorbox{black!10}{#1}}
```

Example usage: `\syntaxHighlight{chapters/contributors.tex}`

![image](https://github.com/DRAMCO/writing-scientific-papers-in-latex-tips-and-tricks/assets/8626571/ef6527a8-d869-48f8-8ba8-6e0fdd42a966)


## Meta

### Finding weird Unicode

Add in the preamble the following to easily find a weird unicode in Overleaf.
```latex
\DeclareUnicodeCharacter{2500}{\color{red} FIX ME!!!!}
```

### Highlight updates or inline comments

```latex
\usepackage[dvipsnames]{xcolor} %required package
\newcommand{\update}[1]{{\color{YellowOrange} #1}} %usage \update{this is changed.}

\usepackage[dvipsnames,svgnames, table]{xcolor} % Required to specify custom colors

\usepackage{listofitems}
\usepackage{pgffor}

\makeatletter
% Define your own list of colors
\def\myColorList{LimeGreen,BrickRed,Fuchsia,Bittersweet,YellowOrange, YellowGreen, WildStrawberry}
\readlist\ColorList\myColorList


\newcommand{\defineauthors}[1]{
    Personal commands for comments are:
    \begin{itemize}
    \foreach \x [count=\xi from 1] in {#1} {   
        \item \textcolor{\ColorList[\xi]}{\textbackslash\unexpanded\expandafter{\x}\{\}}
        }
    
    \end{itemize}

    \foreach \x [count=\xi from 1] in {#1} { 
    \expandafter\xdef\csname\x\endcsname####1{\noexpand\textcolor{\ColorList[\xi]}{[\unexpanded\expandafter{\x}: ####1]}}%
    }
}
\makeatother

%usage after begin document
\defineauthors{all, gilles, emma, ozlem, lianet, nicola}
```

![image](https://github.com/DRAMCO/writing-scientific-papers-in-latex-tips-and-tricks/assets/8626571/41b378a5-7219-4988-a46a-e7e4288ca9ba)



## Math

Typesetting and defining symbols:
```latex
\usepackage{xifthen}
\newcommand{\prob}[1][]{%requires xifthen package%
\ifthenelse{\isempty{#1}}%
      {\ensuremath{P}}%
    {\ensuremath{P\left\(#1\right\)}}%
}
\newcommand{\vect}[1]{\boldsymbol{\mathrm{#1}}}
\newcommand{\mat}[1]{\boldsymbol{\mathrm{#1}}}
\newcommand{\MSE}{\mathrm{MSE}}
\newcommand{\tr}{\mathrm{tr}}
\newcommand{\moddef}{\mathrm{mod}}
\newcommand{\diag}{\mathrm{diag}}
\newcommand{\vecop}{\text{vec}}
\newcommand{\CP}{L}
\newcommand{\hddots}{\hdots}
\newcommand*{\inC}[1]{\in\mathbb{C}^{#1}}
\newcommand{\norm}[1]{\left\lVert#1\right\rVert}
\newcommand{\abs}[1]{\left\lvert#1\right\rvert}
\newcommand{\expt}[1]{\mathbb{E} \left\{#1\right\}}
\newcommand{\cn}[2]{\ensuremath{\sim\mathcal{C}\mathcal{N}\left(#1,#2\right)}}
```


## Glossaries

```latex
\usepackage[xindy, toc, numberedsection, acronym]{glossaries}
\usepackage{hyperref}
\loadglsentries{abbr.tex}
\makeglossaries 
```

More information: https://www.overleaf.com/learn/latex/Glossaries
Base LaTex file is located [here](https://github.com/GillesC/abbreviations-latex).

Scripting files to format the file, remove duplicates, merge different abbr files is located [here](https://github.com/GillesC/abbreviations-latex).



## Bibliography

### Clean bib files

- Clean-up your bib files: https://flamingtempura.github.io/bibtex-tidy/
- I also always enable the "Enclose values in double braces" option to keep the capitalization in titles.
- [My default setup](https://flamingtempura.github.io/bibtex-tidy/index.html?opt=%7B%22modify%22%3Atrue%2C%22omit%22%3A%5B%22abstract%22%2C%22keywords%22%2C%22abstractnote%22%2C%22note%22%5D%2C%22curly%22%3Atrue%2C%22numeric%22%3Atrue%2C%22months%22%3Afalse%2C%22space%22%3A2%2C%22tab%22%3Atrue%2C%22align%22%3A13%2C%22blankLines%22%3Afalse%2C%22sort%22%3A%5B%22key%22%5D%2C%22duplicates%22%3A%5B%22key%22%2C%22doi%22%2C%22citation%22%2C%22abstract%22%5D%2C%22stripEnclosingBraces%22%3Afalse%2C%22dropAllCaps%22%3Afalse%2C%22escape%22%3Atrue%2C%22sortFields%22%3A%5B%22title%22%2C%22shorttitle%22%2C%22author%22%2C%22year%22%2C%22month%22%2C%22day%22%2C%22journal%22%2C%22booktitle%22%2C%22location%22%2C%22on%22%2C%22publisher%22%2C%22address%22%2C%22series%22%2C%22volume%22%2C%22number%22%2C%22pages%22%2C%22doi%22%2C%22isbn%22%2C%22issn%22%2C%22url%22%2C%22urldate%22%2C%22copyright%22%2C%22category%22%2C%22note%22%2C%22metadata%22%5D%2C%22stripComments%22%3Atrue%2C%22trailingCommas%22%3Afalse%2C%22encodeUrls%22%3Afalse%2C%22tidyComments%22%3Atrue%2C%22removeEmptyFields%22%3Atrue%2C%22removeDuplicateFields%22%3Atrue%2C%22lowercase%22%3Atrue%2C%22enclosingBraces%22%3A%5B%22title%22%5D%2C%22backup%22%3Atrue%7D)

### Use Biblatex
No cite or natbib package is required. For more info check: `https://www.overleaf.com/learn/latex/Bibliography_management_with_biblatex`.
Always be aware there is a difference in citation style and bibliography style.

```latex
\usepackage[backend=biber,style=ieee]{biblatex}
%\usepackage[backend=biber,language=dutch]{biblatex}
\addbibresource{bib.bib}
\AtBeginBibliography{\footnotesize}

\begin{document}

\printbibliography
\end{document}

```


## Tables
- Handy table generator: https://www.tablesgenerator.com/
- I prefer to use the Booktabs table style. An example can be found in the following link: https://nhigham.com/2019/11/19/better-latex-tables-with-booktabs/
- 
### Hide columns
```latex
%% to hide a column in table 
\usepackage{array}
\newcolumntype{H}{>{\setbox0=\hbox\bgroup}c<{\egroup}@{}}
```

## SI-units

```latex
\usepackage[per-mode=symbol]{siunitx}  %usage \SI{35}{\meter\squared}
\DeclareSIUnit{\dBm}{dBm}	% add SI unit "dBm"
```

## Clever reference

```latex
\usepackage[capitalise]{cleveref}  %usage \cref{fig:figureReference}
```
- Standard figure reference gives (\ref) gives: 1
- Cleveref figure references gives (\cref): fig. 1

## Figures

### ETH Figure Tool 

![ETH Figure Tool](https://www.bsaver.io/misc/pretty-figures)

### Python to Tikz

tikzplotlib

### Extract data from existing figures

https://automeris.io/WebPlotDigitizer/

![](https://automeris.io/WebPlotDigitizer/images/wpd-scaled.png)

### Indicate lines in a plot

```latex
%draw arc
\draw (x0, y0) arc
    [
        start angle=50,
        end angle=310,
        x radius=0.1cm,
        y radius =0.6cm
    ] ;
    
%draw line 
\draw[] (x1, y1) -- (x2, y2);

%add text
\node[] (x3,  y3) {my text};
```

example: 

![My Image](figs/arc_example.PNG)

## Preparing for submission

### Clean-up Project

[LaTeX cleaner](https://github.com/google-research/arxiv-latex-cleaner/) from Google Research.

Usage: 
```bash
pip install arxiv_latex_cleaner
arxiv_latex_cleaner ./ --keep_bib --verbose
tar -jcvf arxiv.tar.gz gwffzkzgrjgpqksqdkfgtvzkfnjwghny_arXiv/
```

#### LaTeX cleaner's main features:
*   Removes all auxiliary files (`.aux`, `.log`, `.out`, etc.).
*   Removes all comments from your code (yes, those are visible on arXiv and you
    do not want them to be). These also include `\begin{comment}\end{comment}`,
    `\iffalse\fi`, and `\if0\fi` environments.
*   Optionally removes user-defined commands entered with `commands_to_delete`
    (such as `\todo{}` that you redefine as the empty string at the end).
*   Optionally allows you to define custom regex replacement rules through a
    `cleaner_config.yaml` file.
    
There is a 50MB limit on arXiv submissions, so to make it fit:

*   Removes all unused `.tex` files (those that are not in the root and not
    included in any other `.tex` file).
*   Removes all unused images that take up space (those that are not actually
    included in any used `.tex` file).
*   Optionally resizes all images to `im_size` pixels, to reduce the size of the
    submission. You can allowlist some images to skip the global size using
    `images_allowlist`.
*   Optionally compresses `.pdf` files using ghostscript (Linux and Mac only).
    You can allowlist some PDFs to skip the global size using
    `images_allowlist`.



### Shortening a Paper

### Reducing space after caption
```latex
\setlength{\belowcaptionskip}{-20pt} % in the preamble
```

#### Biblatex hacks
- You can check how many times a certain reference is cited in the text. In this example, every reference which is only cited once is colored red. 
```latex
\usepackage[backend=biber, style=ieee, citestyle=numeric-comp, maxcitenames=1,mincitenames=1, maxbibnames=1, minbibnames=1,isbn=false, doi=false,citecounter=true]{biblatex}
\addbibresource{bib.bib}
\AtBeginBibliography{\footnotesize}
\renewcommand{\finentrypunct}{%
  \addperiod\space
  \ifnum \value{citecounter} < 2
  \color{red}
  \else
   \color{Green}
    \fi
  (Cited \arabic{citecounter})%
}
```
- The number of names shown in the bibliography can be altered by the `maxbibnames=1, minbibnames=1` option.
- What if linebreaking of titles in bibliography not working correctly. Possible solutions:
	- remove \usepackage{ulem}
   	- remove \usepackage{cite}
	- remove \usepackage{natbib}
 
## Updating manuscript
### Change color of single reference using biblatex

```latex
% Example bib entry
@article{biodegradables,
	title        = {{Recent Advances in Biodegradable Green Electronic Materials and Sensor Applications}},
	author       = {Min, JinKi and Jung, Yeongju and Ahn, Jiyong and Lee, Jae Gun and Lee, Jinwoo and Ko, Seung Hwan},
	year         = 2023,
	journal      = {Advanced Materials},
	volume       = 35,
	number       = 52,
	pages        = 2211273,
	doi          = {https://doi.org/10.1002/adma.202211273},
}
```

```latex
% Define start and reset color
\makeatletter
\newcommand{\startcolor}{%
  \color{RoyalBlue}\global\let\default@color\current@color
}
\newcommand{\resetcolor}{%
  \color{black}\global\let\default@color\current@color
}
\makeatother

% Make a highlighted category
\DeclareBibliographyCategory{highlighted}

% Add specific bib entries to category
\addtocategory{highlighted}{biodegradables}
\addtocategory{highlighted}{other_bib_item}
\addtocategory{highlighted}{another_bib_item}

\AtEveryBibitem{%
  \ifcategory{highlighted}{\startcolor}{\resetcolor}
}
```
