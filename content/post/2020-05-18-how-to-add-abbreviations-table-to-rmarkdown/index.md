---
title: How to Add Abbreviations Table to Rmarkdown
author: Roel M. Hogervorst
date: '2020-05-18'
slug: how-to-add-abbreviations-table-to-rmarkdown
categories:
  - r
tags:
  - formatting
  - rmarkdown
  - academic
---


Quick tip if you write a lot rmarkdown documents and you want to add abbreviations
add the folling bit to the top. Its auto sorted too.

```r
library(tidyverse)
tibble::tribble(
    ~abbreviation, ~meaning,
   "ZZA", "Ze Zoom Abbreviation",
    "tribble", "a row wise tibble"
) %>% 
    arrange(abbreviation) %>%
    knitr::kable(caption = "abbreviations")
```    
