---
title: Add a wrapper around functions you call in map
author: Roel M. Hogervorst
date: '2017-11-17'
slug: add-a-wrapper-around-functions-you-call-in-map
categories:
  - R
tags:
  - hacks
  - purrr
difficulty:
  - advanced
post-type:
  - lessons-learned
subtitle: "and give yourself feedback"
---

I recently wanted to download hundreds of files
However I had to wait for a long time, didn't know how far I was (could have checked the folder)

A solution to help me, because I'm easily bored, is to get feedback on the progress.
I wrapped a messaging function around the download function, that I called many 
times.

```
#' download a file and give feedback
download_file <- function(file){
    filename <- basename(file)
    if(file.exists(paste0("data/",filename))){
        print(paste("file exists: ",filename))
    }else{
        print(paste0("downloading file:", file))

        curl::curl_download(url = file,destfile = paste0("data/",filename),mode = "wb")
        Sys.sleep(0.3)
    }
}
```

I then apply the function to a list of web adresses:


```
map(paste0("first part of the link",
           formatC(1:latest_episode, width = 3,flag = 0),".txt"), download_file)
```

**!!!! The bottleneck was here not in the repetition, but in me, I am not a patient man. I wrapped the same functionality around readr::read_lines and it was horribly slow!**

example:

```
read_lines2 <- function(file){
    print(file)
    read_lines(file)
}

## read_lines2: user 2.00, system 1.71, elapsed 17.32
## read_lines: user 0.61, system 1.05, elapsed 1.69  (crazy slowdown by print!)
```
~fin
