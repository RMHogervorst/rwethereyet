---
title: Display all Functions in an R Package
author: Roel M. Hogervorst
date: '2020-06-01'
slug: display-all-functions-in-an-r-package
categories:
  - r
tags:
  - package
---

Something I keep forgetting: How do you display all the user facing functions from a package?


On [stackoverflow](https://stackoverflow.com/questions/20535247/how-to-find-all-functions-in-an-r-package) I found the following answers:

This function displays all the functions and their arguments
```r
# needs to be active, using library(packagename)
lsf.str("package:pinboardr")
```
result:

```
pb_add_tag_column : function (dataframe, tag)  
pb_get_note : function (id = NULL, username = NULL, token = NULL)  
pb_get_notes_overview : function (username = NULL, token = NULL)  
pb_last_update : function (as_datetime = FALSE, username = NULL, token = NULL)  
pb_posts_add : function (url, title, description = NULL, tags = NULL, dt = NULL, replace = NULL, public = NULL, 
    toread = NULL, username = NULL, token = NULL)  
```

Best option I think is `getNamespaceExports()`

```r
getNamespaceExports("pinboardr")
```
which results in function names.
```
 [1] "pb_add_tag_column"     "pb_get_note"           "pb_get_notes_overview" "pb_last_update"       
 [5] "pb_posts_add"          "pb_posts_all"          "pb_posts_dates"        "pb_posts_delete"
 ```
