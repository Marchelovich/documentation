---
title: Pie Charts in R | Examples | Plotly
name: Pie Charts
permalink: r/pie-charts/
description: How to make pie charts in R using plotly.
layout: base
thumbnail: thumbnail/pie-chart.jpg
language: r
page_type: example_index
has_thumbnail: true
display_as: chart_type
order: 7
output:
  html_document:
    keep_md: true
---


### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.

```r
library(plotly)
packageVersion('plotly')
```

### Basic Pie Chart


```r
library(plotly)

USPersonalExpenditure <- data.frame("Categorie"=rownames(USPersonalExpenditure), USPersonalExpenditure)
data <- USPersonalExpenditure[,c('Categorie', 'X1960')]

plot_ly(data, labels = ~Categorie, values = ~X1960, type = 'pie') %>%
  layout(title = 'United States Personal Expenditures by Categories in 1960',
         xaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE),
         yaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE))
```

```
## Warning in arrange_impl(.data, dots): '.Random.seed' n'est pas un vecteur
## d'entiers, mais est de type 'NULL', et sera donc ignoré
```



### Styled Pie Chart


```r
library(plotly)

USPersonalExpenditure <- data.frame("Categorie" = rownames(USPersonalExpenditure), USPersonalExpenditure)
data <- USPersonalExpenditure[, c('Categorie', 'X1960')]

colors <- c('#F85F73', '#FECEA8', '#928A97', '#283C63', '#392F2F')

plot_ly(data, labels = ~Categorie, values = ~X1960, type = 'pie',
        textposition = 'inside', 
        textinfo = 'label+percent',
        insidetextfont = list(color = '#FFFFFF'),
        hoverinfo = 'text', 
        text = ~paste('$', X1960, ' billions'),
        marker = list(colors = colors,
                      line = list(color = '#FFFFFF', width = 1)),
                      #The 'pull' attribute can also be used to create space between the sectors
        showlegend = FALSE) %>%
  layout(title = 'United States Personal Expenditures by Categories in 1960',
         xaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE),
         yaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE))
```



### Subplots


```r
library(plotly)
library(dplyr)

plot_ly() %>%
  add_pie(data = count(diamonds, cut), labels = ~cut, values = ~n,
          name = "Cut", domain = list(x = c(0, 0.4), y = c(0.4, 1)),
          textinfo = 'label+percent') %>%
  add_pie(data = count(diamonds, color), labels = ~color, values = ~n,
          name = "Color", domain = list(x = c(0.6, 1), y = c(0.4, 1)),
          textinfo = 'label+percent') %>%
  add_pie(data = count(diamonds, clarity), labels = ~clarity, values = ~n,
          name = "Clarity", domain = list(x = c(0.25, 0.75), y = c(0, 0.6)),
          textinfo = 'label+percent') %>%
  layout(title = "Pie Charts with Subplots", showlegend = F,
         xaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE),
         yaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE))
```



See more examples of subplots [here](https://plot.ly/r/subplots/).

### Donut Chart


```r
library(plotly)

# Get Manufacturer
mtcars$manuf <- sapply(strsplit(rownames(mtcars), " "), "[[", 1)

mtcars %>%
  group_by(manuf) %>%
  summarize(count = n()) %>%
  plot_ly(labels = ~manuf, values = ~count, textinfo = 'label+percent') %>%
  add_pie(hole = 0.6) %>%
  layout(title = "Donut charts using Plotly",  showlegend = F,
         xaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE),
         yaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE))
```



#Reference

See [https://plot.ly/r/reference/#pie](https://plot.ly/r/reference/#pie) for more information and chart attribute options!