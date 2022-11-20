---
title: Issue with BigQuery 
author: Roel M. Hogervorst
date: '2017-11-17'
slug: issue-error-in-readrds-bigquery
categories:
  - r
tags:
  - solution
  - bigquery
  - readrds
  - error
difficulty:
    - advanced
post-type:
  - lessons-learned
---

I had a problem with bigrquery that I couldn't figure out.

    * my laptop crashed (happens sometimes)
    * this corrupted (I think) the .httr-oauth file in my folder
    * the error I received was extremely not helpful:

```
Error in readRDS(cache_path) :
  ReadItem: unknown type 97, perhaps written by later version of R
```

Solution: delete the .httr-oath token

What I instead did:

- remove the rstudio files
- check if there were similar issues with bigrquery (nope)
- find if there was a ~/.Rdata file (There wasn't)
- remove hidden rstudio project files
- remove .RProject file

I could not find a simple answer online so I'm recording this for the future.
