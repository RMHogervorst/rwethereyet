---
title: Linewidth
author: Roel M. Hogervorst
date: '2020-05-31'
slug: linewidth
categories:
  - other
tags:
  - 100DaysToOffload
  - programming
  - python
subtitle: ''
---

It seems the linewidth wars are starting up again. 

![(picture from undraw)](/2020-05-31-linewidth/index_files/undraw_proud_coder_7ain.png)


Linus Torvalds [speaks (characteristicly harsh, but not super rude)](https://lkml.org/lkml/2020/5/29/1038) about restricting
your code to a linewidth of 80, he says it is nonsense. 

- basic tools like grep are line based and break if you break your lines
- monitors are wide
- we no longer live in the 80s


It is a small thing of annoyance for me when the python tools like flake8 or black complain about line length of 80. I usually set it to 120.  


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 6/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
