---
title: 'Solving ''Libxt.so.6: Cannot Open Shared Object'' in grDevices::grSoftVersion()'
author: Roel M. Hogervorst
date: '2020-09-23'
slug: solving-libxt-so-6-cannot-open-shared-object-in-grdevices-grsoftversion
categories:
  - r
tags:
  - r
  - ubuntu
  - docker
  - rocker
  - dependencies
---

This is a small troubleshooting solution I had while building a docker container on rocker/r-ver:latest  (rocker/r-ver:4.0.2)

### Problem
I had a script that created a picture with ggsave. 
However it seemed to fail on an obscure reason:

```
Warning message:
In grDevices::grSoftVersion() :
  unable to load shared object '/usr/local/lib/R/modules//R_X11.so':
  libXt.so.6: cannot open shared object file: No such file or directory
```

First of all this should be an error and not a warning. There is no png file created (this grSoftVersion() function is probably called in `ggplot2::ggsave()`). 
Secondly, I don't know why it isn't in the container. Probably to keep it lightweight. 

### Information about the environment
I have used the rocker container r-verse:4.0.2 (latest R version) which is build on 

- (`cat /etc/issue`) ubuntu 20.04 LTS
- (`cat etc/debian_version`) bullseye/sid
- (`cat /etc/os-release`) focal fossa 

### Solution
What I did was add a missing apt package:
`(sudo) apt-get install libxt6`

Or in docker language
`RUN apt-get install -y --no-install-recommends libxt6`

This finally fixed the issue that I tried to solve for 2 days.

