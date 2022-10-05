# Writing scientific papers in LaTex (Tips and Tricks)

## General




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



<details>
<summary>Bibliography</summary>
<!--All you need is a blank line-->

    + Clean-up your bib files: https://flamingtempura.github.io/bibtex-tidy/
    + I also always enable the "Enclose values in double braces" option to keep the capitalization in titles.
</details>





## Figures

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
