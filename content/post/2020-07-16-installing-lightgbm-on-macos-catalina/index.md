---
title: Installing lightGBM on Macos Catalina
author: Roel M. Hogervorst
date: '2020-07-16'
slug: installing-lightgbm-on-macos-catalina
categories:
  - r
tags:
  - lightgbm
  - boostedtreemethods
  - howto
  - 100DaysToOffload
---

In this walkthrough I 
install lightgbm on the latest version of R on an older model macBook Pro with 
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
I'm following the instructions at [lightgbm.readthedocs.io](https://lightgbm.readthedocs.io/en/latest/R/index.html#mac-os-preparation) *and you should too*.

First I download the code to my computer:

```
git clone --recursive https://github.com/microsoft/LightGBM
```

<details>
<summary> I had an issue `pyenv: gettext.sh: command not found` if you have that
too, you might want to read this hidden text, otherwise skip it. **click here to expand**

</summary>
For some reason this process failed because of my python environment.
This can sometimes happen; 
*I believe the issue is that all shell scripts and python thingies in the python installed  folder are globally active and added to PATH.* 
I'm using pyenv and I have `pyenv: gettext.sh: command not found`
I tried several things, for instance upgrading git in homebrew `brew upgrade git`
but what finally did the trick was deleting my anaconda distribution 
`pyenv uninstall anaconda3-2019.03` . I believe that deleting the gettext part 
in that distribution is also sufficient. 

I deleted the lightGBM folder and re ran the git clone command.

</details>

Continuing the installation: going into the lightGBM folder
and executing the `build_r.R` script.

```
cd LightGBM
Rscript build_r.R
```
And a failure, I do not have openMP (a multithreading library) installed `brew install libomp`. 
I did have it installed, it seems, but it wasn't linked `brew link --overwrite libomp`.
This was a bit aggressive, it overwrites all links to libomp. I may have broken 
things later, but the installation continues and is successful.

(Re)start your R session and check if you can load the library `library(lightgbm)`.

## Installing on multiple R versions using RSwitch
I than used RSwitch to switch R version to an older version of R and 
reran the `Rscript build_r.R` command in the same folder. 
The process reruns the installation and because RSwitch switches the R version
the package is now installed in the older R version location: 
the script spews out 
`* installing to library ‘/Library/Frameworks/R.framework/Versions/4.0/Resources/library’`

(Re)start your R session and check if you can load the library `library(lightgbm)`.
once finished and verified
I switch to R3.6 and rerun the script again.
It now installs in 
`* installing to library ‘/Library/Frameworks/R.framework/Versions/3.6/Resources/library’`


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
