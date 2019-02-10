---
title: 'Creating a bot that tweets old articles on your timeline'
author: Roel M. Hogervorst
date: '2019-02-10'
slug: a-bot-that-tweets-old-articles-on-your-timeline
categories:
  - inspiration
tags:
  - twitter
  - bot
  - go
  - AWS
  - lambda
---

Awesome coder Vicki Lai created a twitter bot for her website that regularly
tweets her older posts. The article is [here](https://vickylai.com/verbose/running-a-free-twitter-bot-on-aws-lambda/).

Some details:

- It runs on AWS lambda (function as a service)
- It's written in GO (R is not supported ...)
- It costs almost nothing
- It uses time as a trigger
- She uses her own RSS feed as source (so it is automatically up to date)
- The function picks a random article from her feed
- the code is here: <https://gist.github.com/vickylai/7859dab68df87e28f40d6715d08383c7>

I wish this could be done in R too. 
But I might borrow her twitter bot and modify it to use my rss feed?
However I might have too long descriptions or no description at all? I'll have
to check.
