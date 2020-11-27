---
title: Decay, Entropy and the Constant Work Required to Keep Things Working
author: Roel M. Hogervorst
date: '2020-11-21'
slug: decay-entropy-and-the-constant-work-required-to-keep-things-working
categories:
  - thoughts
tags:
  - 100DaysToOffload
  - software
subtitle: ''
---


Ever notice how much work goes into just keeping things working? 
I recently read Scott Chamberlains post [fulltext: Behind the Scenes](https://ropensci.org/technotes/2020/11/17/fulltext-story/)  about
the package fulltext, a package for textmining scholarly work. 

The public knowledge of the world is hidden in articles behind paywalls. But if you have access through an academic institute you can 
do super interesting work on the full texts of these articles.

In the post, Scott describes the steps they took

To get a full text article

* use crossref api to go from DOI to published sources

> Given the opportunity to not add links, many publishers do not, and many publishers do not update links once deposited. This leads to many missing links and to errors in existing ones.

* tried out a middle service, that kept links up to date (but this meant keeping up a new dependency)
* tried out mapping in a new R package
* but decided against it, because the review process on CRAN takes a long time compared to submition of new packages.

(So they loaded up a lot of technical dept)

I think it serves as a good demonstration of the complexity and frustration baked into the publishing industry, as well as the trade-offs of various approaches to solving problems and getting things done.

The amount of work that goes into maintaining this work is enourmous. 
what doesn't help: publishers have absolutely nothing to gain from keeping up 
stable, standardized apis. The make money in one way by keeping a stranglehold
on university libraries. Your researchers want to access this so they have to
jump through multiple hoops to get to an article. It took ages before there was
even a standardized way to refer to unique articles. Now it is finally there
(Digital Object Identifyers; DOIs), but publishers still make you jump through three different portals just
to make sure you can access an article. No wonder sci-hub is so popular, it 
just works!



* [(_backup for the article, if the article ever goes down here_)](https://web.archive.org/web/20201117153951/https://ropensci.org/technotes/2020/11/17/fulltext-story/)

*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 41/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
