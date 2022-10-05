# Writing scientific papers in LaTex (Tips and Tricks)

## General


## Figures

### Indicate lines in a plot

```
%draw arc
\draw (x, y) arc
    [
        start angle=50,
        end angle=310,
        x radius=0.1cm,
        y radius =0.6cm
    ] ;
    
%draw line 
\draw[] (x, y) -- (-1, 17);

%add text
\node[] (x,  y) {my text};
```

example: 

![My Image](figs/arc_example.PNG)