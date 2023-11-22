---
title: 'Dagster: Preventing OOM on Multiprocessor Runs'
author: Roel M. Hogervorst
date: '2023-11-22'
slug: dagster-preventing-oom-on-multiprocessor-runs
categories:
  - blog
tags:
  - dagster
  - 100DaysToOffload
  - fan-out
  - TIL
subtitle: ''
difficulty:
  - advanced
post-type:
  - lessons-learned
---

I had a problem in dagster, some jobs had an out of memory error.

My setup is like this
- kubernetes deployment
- every job runs in a kubernetes job
- that means that all ops run in that container in a separate python proces

The processes are not aware of each other and I had a beautiful fan-out pattern and so the container got out of memory.

I first tried to increase memory for peak memory usage on that job, but there is a more elegant solution. You can limit the amount of ops that run concurrently

according to [the docs](https://docs.dagster.io/guides/limiting-concurrency-in-data-pipelines#limiting-overall-concurrency-in-a-job) you can annotate a job:

```python
@job(
    config={
        "execution": {
            "config": {
                "multiprocess": {
                    "max_concurrent": 4}
                    }
                }
            })
def an_interesing_job():
    ...
```


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 32/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
