---
title: All Run Requests from One Sensortick Use the Same Container Image
author: Roel M. Hogervorst
date: '2022-09-03'
slug: all-run-requests-from-one-sensortick-use-the-same-container-image
categories:
  - lessons-learned
tags:
  - dagster
  - TIL
---

Quick lesson learned in the past weeks. For one of our clients we use Dagster as an orchestrator. 

I had a sensor that kicked off 2000 runs. That is OK, because I limit the max of concurrent jobs. All the requests go into a queue and dagster will  work through the queue and spin up new jobs when old ones are done. 

There was a bug that was caused mostly by me not testing the code. 
(the ease of testing was one of the reasons to choose dagster over airflow, but you still have to write the tests).


After the jobs were kicked off (and moved into the queue) we continued work and released a patch that fixed the bug I introduced earlier.
But the new runrequests (jobs) did not pick up this code change.
We had thousands of runs failing.

My mental model of a sensor and runrequests going in was:
- every run that gets kicked off reads from the repository as is. 



What i learned was: the runrequests do not only save what repo and what job, but also what containerversion. It kept pulling the old container without changed code.
