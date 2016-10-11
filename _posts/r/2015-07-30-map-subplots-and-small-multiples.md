---
title: Map Subplots And Small Multiples
name: Map Subplots And Small Multiples
permalink: r/map-subplots-and-small-multiples/
description: How to create map subplots and small multiples in R.
layout: base
thumbnail: thumbnail/map-subplots.jpg
language: r
page_type: example_index
has_thumbnail: true
display_as: maps
output:
  html_document:
    keep_md: true
---



### Basic Subplots with Maps


```r
library(plotly)
library(dplyr)
df <- read.csv('https://raw.githubusercontent.com/plotly/datasets/master/1962_2006_walmart_store_openings.csv')

# common map properties
g <- list(
  scope = 'usa',
  showland = T,
  landcolor = toRGB("gray90"),
  showcountries = F,
  subunitcolor = toRGB("white")
)

one_map <- function(dat) {
  plot_geo(dat) %>%
    add_markers(x = ~LON, y = ~LAT, color = I("blue"), alpha = 0.5) %>%
    add_text(x = -78, y = 47, text = ~unique(YEAR), color = I("black")) %>%
    layout(geo = g)
}

df %>%
  group_by(YEAR) %>%
  do(map = one_map(.)) %>%
  subplot(nrows = 9) %>%
  layout(
    showlegend = FALSE,
    title = 'New Walmart Stores per year 1962-2006<br> Source: <a href="http://www.econ.umn.edu/~holmes/data/WalMart/index.html">University of Minnesota</a>',
    width = 1000,
    height = 900,
    hovermode = FALSE
  )
```

<iframe src="https://plot.ly/~RPlotBot/3173.embed" width="800" height="900" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>