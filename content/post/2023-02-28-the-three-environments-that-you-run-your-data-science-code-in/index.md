---
title: The Three Environments that you Run your Data Science Code in
author: Roel M. Hogervorst
date: '2023-02-28'
slug: the-three-environments-that-you-run-your-data-science-code-in
categories:
  - blog
tags:
  - data science
  - coding skills
  - testing
difficulty:
  - beginner
post-type:
  - post
---

There are three environments where you need to run your code; locally (a notebook for example), test (to make sure your code does what it should do) and production (to do the actual work).


**Local** is for you to iterate fast. To experiment with new models and different features. 


**Test** is to make sure you don't make the same mistake twice _(when you find a mistake, capture the behavior in a test to make sure it doesn't happen again)_. Why do I call this a different environment?
When you run unit tests, ideally they should be able to be run in parallel. If you design your code so it is easy to test, it is often easy to change too!


**Production** is what you do it all for. One of the reasons you write tests. You write code so it does work for you. Wherever that happens is production.  

