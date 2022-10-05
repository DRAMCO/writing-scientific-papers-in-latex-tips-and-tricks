# Writing scientific papers in LaTex (Tips and Tricks)

## General

## Bibliography

Clean-up your bib files: https://flamingtempura.github.io/bibtex-tidy/

I also always enable the "Enclose values in double braces" option to keep the capitalization in titles.


## Figures

### Extract data from existing figures

https://automeris.io/WebPlotDigitizer/

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
