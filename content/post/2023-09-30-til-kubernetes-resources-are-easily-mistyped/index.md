---
title: 'TIL: Kubernetes Resources are Easily Mistyped'
author: Roel M. Hogervorst
date: '2023-09-30'
slug: til-kubernetes-resources-are-easily-mistyped
categories:
  - blog
tags:
  - 100daystooffload
  - kubernetes
  - helm
  - TIL
subtitle: "Why won't the system give me 500.000 cpus?"
difficulty:
  - advanced
post-type:
  - lessons-learned
---

At $work we have a kubernetes[^1] cluster. I have to tell every deployment
how many resources we need, if you go over a certain threshold the deployment
is refused. 

I wanted half a CPU (500 millicpu) but my deployment was refused: "You are not 
allowed to claim 500.000 cpus". 

You know why?

- I claimed "500M" in stead of "500m"

I wonder if that is ever needed?



[^1]: I heard someone call it 'kates,' based on the k8s acronym I guess?

*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 13/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
