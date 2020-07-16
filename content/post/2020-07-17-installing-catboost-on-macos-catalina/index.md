---
title: Installing Catboost on MacOS Catalina
author: Roel M. Hogervorst
date: '2020-07-17'
slug: installing-catboost-on-macos-catalina
categories:
  - r
tags:
  - 100DaysToOffload
  - boostedtreemethods
  - catboost
---

In this walkthrough I 
install catboost on the latest version of R on an older model macBook Pro with 
Macos Catalina 10.15.5 and I'm using homebrew. 

The world of boosted tree models is growing over the past 4 years, the first
revolution was with 'XGBoost' (eXtreme Gradient Boosting) in 2016, followed by 
'lightGBM' (or LGBM) from January 2017 and later that year 'catboost'. To use
these C++ libraries in R you have to install them, and that process is slightly
different for different architectures.

## Prep
I'm also using the amazing [RSwitch tool](https://rud.is/rswitch/) for the Mac
to switch R versions: from 4.1.0 "experimental version", to the latest stable version 
R 4.0.2 'Taking off again' and an older version before 
that R 3.6.3 (2020-02-29) 'Holding the Windsock'.
I'm trying to install this library on all R versions, but if you use one version 
of R, this RSwitch tool is not necessary.

I'm mentioning all this because sometimes these things are really difficult to
debug under different operating systems, and different R versions.
For work I installed lightGBM on a macbook a year ago, and it was a lot more work then. 

## Installation
I've never installed catboost before so let's see how it goes.

Catboost creates releases (bless them!) that you can install on you computer.

I followed the instruction for binary installation 
[here on catboost.ai](https://catboost.ai/docs/installation/r-installation-binary-installation.html#r-installation-binary-installation).

You go to the releases page and find the release you want, the latest I think

For me the instructions were:
```r
devtools::install_url('https://github.com/catboost/catboost/releases/download/v0.23.2/catboost-R-Darwin-0.23.2.tgz', INSTALL_opts = c("--no-multiarch"))
```
Please do verify that the links is correct for you, the version might have updated
or you might point to different software. Another way to install this is
to download the tgz file, inspect it with a virus scanner and use 
`remotes::install_local()` 

(Re)start your R session and check if you can load the library `library(catboost)`.

## Installing on multiple R versions using RSwitch
Use RSwitch to switch R version to an older version of R and rerun the
devtools argument above. 
(Re)start your R session and check if you can load the library `library(catboost)`.
repeat for all versions of R you want to check

And you are done.


# Fin
I thought there would be issues with different versions of R, but the main issues
are related to architecture: system libraries that you have to install on macos.
After this installation the installation of the R wrapper is not really a big
issue anymore, at least not for R 3.6, 4.0 and 4.1 (at the time of writing).

### References
- Find more polished R tutorials by me in [this tutorial overview page on my main blog feed](https://blog.rmhogervorst.nl//tags/tutorial/)
- [latest lightgbm page (specific link to mac part)](https://lightgbm.readthedocs.io/en/latest/R/index.html#mac-os-preparation)
- [RSwitch tool](https://rud.is/rswitch/)
- find other posts about these gradient boosted tree methods on this website under the tag [boostedtreemethods](https://notes.rmhogervorst.nl/tags/boostedtreemethods/)

*I’m publishing this post too as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 16/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
