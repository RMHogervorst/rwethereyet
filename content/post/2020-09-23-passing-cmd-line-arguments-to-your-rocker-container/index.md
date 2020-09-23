---
title: Passing Cmd Line Arguments to your Rocker Container
author: Roel M. Hogervorst
date: '2020-09-23'
slug: passing-cmd-line-arguments-to-your-rocker-container
categories:
  - r
tags:
  - docker
  - r
  - variables
---


Quick thingy: For a Rocker (Docker containers with R installed) project I have to pass environmental variables. How do you pass that to the container? I save env variables for R to a .Renviron file. That way the R process can search for these vars and you do not have to hardcode them in the script. 

Now saving it in a local .Renviron file has two effects:
It is easy to pass to the container, you can run the script locally too. 


Steps:

* First you build the container:

`docker build -t <name> .`

* then you run the image and pass the variables in the form of a file:

`docker run --env-file .Renviron <name>`

done
