---
title: 3D Line Plots in R | Examples | Plotly
name: 3D Line Plots
permalink: r/3d-line-plots/
description: How to make interactive 3D line plots in R.
layout: base
thumbnail: thumbnail/3d-line.jpg
language: r
page_type: example_index
has_thumbnail: true
display_as: 3d_charts
order: 2
output:
  html_document:
    keep_md: true
---



# 3D Line Plots in R


```r
# initiate a 100 x 3 matrix filled with zeros
m <- matrix(numeric(300), ncol = 3)
# simulate a 3D random-walk
for (i in 2:100) m[i, ] <- m[i-1, ] + rnorm(3)
# collect everything in a data-frame
df <- setNames(
  data.frame(m, seq(1, 100)),
  c("x", "y", "z", "time")
)
library(plotly)
plot_ly(df, x = ~x, y = ~y, z = ~z, color = ~time) %>% add_lines()
```

<iframe src="https://plot.ly/~RPlotBot/3054.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>