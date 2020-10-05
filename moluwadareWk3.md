EXPLORING THE PLOTLY USING BREAST CANCER DATA
========================================================
author: OLUWADARE MARGARET
date: 30TH SEPTEMBER, 2020
autosize: true
INTRODUCTION
========================================================
Dr. William H. Wolberg of the University of Wisconsin pioneered the
Wisconsin Breast Cancer Data in 1990. His goal of collecting the data was to identify
whether a tumor biopsy was malignant or benign. His team collected the samples
using Fine Needle Aspiration (FNA). Our aim here is to demonstrate the use of `plotly` in plotting this data set.

To do this we will access the `Mass` library and read in the data called `biospy`. The following till be carried out:

- Read in the data
- Relabel varaiable names
- Perform some data cleaning and exploration
- Plot the data using `plotly`

PREPARE THE ENVIRONMENT
========================================================
 The following library will be used and the `biospy` data set from the `MASS` library will be used. 


```r
library(MASS); library(corrplot); library(ggplot2); library(tidyverse);
library(plotly)
library(rgl); library(rglwidget)
data(biopsy)
```
We perform some cleaning by removing the `id` variable, renaming the varaible and ommiting `na's`.


```r
bc <- biopsy[-1]
names(bc) <- c("age", "mnp", "ts", "inv", "ndc", "deM", "breast", "brtq", "irat", "class" )
bc = na.omit(bc)
str(bc)
```

```
'data.frame':	683 obs. of  10 variables:
 $ age   : int  5 5 3 6 4 8 1 2 2 4 ...
 $ mnp   : int  1 4 1 8 1 10 1 1 1 2 ...
 $ ts    : int  1 4 1 8 1 10 1 2 1 1 ...
 $ inv   : int  1 5 1 1 3 8 1 1 1 1 ...
 $ ndc   : int  2 7 2 3 2 7 2 2 2 2 ...
 $ deM   : int  1 10 2 4 1 10 10 1 1 1 ...
 $ breast: int  3 3 3 3 3 9 3 3 1 2 ...
 $ brtq  : int  1 2 1 7 1 7 1 1 1 1 ...
 $ irat  : int  1 1 1 1 1 1 1 1 5 1 ...
 $ class : Factor w/ 2 levels "benign","malignant": 1 1 1 1 1 2 1 1 1 1 ...
 - attr(*, "na.action")= 'omit' Named int [1:16] 24 41 140 146 159 165 236 250 276 293 ...
  ..- attr(*, "names")= chr [1:16] "24" "41" "140" "146" ...
```

PLOT OF DATA
========================================================

```r
# Point colors
marker <- list(color = ~class, colorscale = c('#FFE1A1', '#683531'), 
               showscale = TRUE)
# Create the plot
p <- plot_ly(bc, x = ~age, y = ~mnp, z = ~brtq, marker = marker) %>%
  add_markers() %>%
  layout(
    scene = list(xaxis = list(title = 'age'),
                 yaxis = list(title = 'menopause'),
                 zaxis = list(title = 'breast quarter'), 
                 title = "Breast cancer Data")
  )
p
```

![plot of chunk Plot](moluwadareWk3-figure/Plot-1.png)
