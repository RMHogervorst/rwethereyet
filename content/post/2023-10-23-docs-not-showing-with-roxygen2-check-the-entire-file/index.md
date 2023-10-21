---
title: Docs not Showing with Roxygen2? Check the Entire File
author: Roel M. Hogervorst
date: '2023-10-23'
slug: docs-not-showing-with-roxygen2-check-the-entire-file
categories:
  - R
tags:
  - TIL
  - 100DaysToOffload
subtitle: ''
difficulty:
  - intermediate
post-type:
  - lessons-learned
---
Recently I had a weird experience with roxygen2. I wanted to create docs for a
piece of code but they were just not showing up!

For some context; I'm the maintainer of the ropensci [{charlatan}](https://github.com/ropensci/charlatan) package that fakes data. 
I am currently working on a major rewrite that will make it much easier to add new
features. Roxygen2 is a package that helps you write documentation. One of its
best features is that you write the docs in the same file as the code, that 
prevents it from going out of date. 
Roxygen is specific for R, but in python you can export docstrings and use
redoc or sphinx to build docs for your software too (there must also be 
jave versions and for other languages too, but I don't write in those languages).


What was the problem?

This is what the top of the file looked like:

```r
#' @title PersonProvider
#' @details Methods for Persons, methods for generating names.
#' @inherit BaseProvider note
#' @family ParentProviders
#' @export
#' @returns A PersonProvider object that can create names. 
PersonProvider <- R6::R6Class(
	...
```
If you have worked with roxygen you will notice
- `@export` tag: so that means export this file in the package
- `@title` and `@details` (not necessary but I like this to be explicit)

This all suggests that the docs should be exported, but they were not.

I finally opened an issue on roxygen and got a fast reply.
I shot myself in the foot again.


Somewhere in this file I had a `@noRd` tag:

```r
...
    #' @description messy switch (internal).
    #' Always return a text, when messy is allowed return a messy
    #' version, but otherwise return a clean version.
    #' @noRd
    #' @param clean_choice the clean version
    #' @param messy_choice the messy version
    messy_switch = function(clean_choice, messy_choice) {
    ...
```

And that tag is valid for the whole manual file. 

So search for `@noRd` when your file does not render!


Gabor also responded with some more details that I had read, but forgot:

> roxygen2 parses the #' comments until the end of the function (or object) definition. This can be quite handy when you want to keep the a piece of the manual page close to the code it documents. E.g. this is an example I like: [r-lib/cli@d888311/R/num-ansi-colors.R#L37](https://github.com/r-lib/cli/blob/d8883112a8060c1f011cccc9147dd35db03bb9c6/R/num-ansi-colors.R#L37)


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 31/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
