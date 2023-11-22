---
title: 'Dagster: Limiting Sensor Runs Might not Solve your Problem'
author: Roel M. Hogervorst
date: '2023-11-23'
slug: dagster-limiting-sensor-runs-might-not-solve-your-problem
categories:
  - blog
tags:
  - dagster
  - 100DaysToOffload
  - TIL
  - queue
subtitle: ''
difficulty:
  - advanced
post-type:
  - lessons-learned
---

We had an issue where we wanted to limit when jobs were kicked off. 
This is relatively easy, you can add a check in the sensor for current time.

However, that does not completely solve the issue. Because the sensor throws
new jobs into the job-queue, but the queue does not care about time, so
if your sensor puts a lot of jobs in the queue and the queue slowly empties
you still have the jobs running when you don't want to run them. 

I don't think there is a way to prevent this from happening.
If you do want to prevent this from happening, you need to change the way
you set up the work, make the jobs run on a schedule in stead of a sensor.

*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 33/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
