---
title: Containers , Cmd not Found
author: Roel M. Hogervorst
date: '2023-10-02'
categories:
  - blog
tags:
  - 100DaysToOffload
  - containers
  - kubernetes
  - TIL
slug: containers-cmd-not-found
subtitle: executable file not found in $PATH
difficulty:
  - intermediate
post-type:
  - lessons-learned
---

Running a container in kubernetes is sometimes annoyingly difficult.
Especially if the feedbackloop is long, when you only get a failing container
notification.


Here is one I had recently:

`OCI runtime exec failed: exec failed: (...) executable file not found in $PATH": unknown`

I knew the container had the thing, so what on earth is going wrong?

In a manifest for kubernetes (deployments/statefulsets etc.) you must specify
a container (of course) but you can also supply a `cmd` and or `args`.

The container that I started already executed a command on start, but by supplying the command
with cmd, the system could not find that part. 

It took me 2 hours but finally it dawned  on me: supply the things in `args`.

Now it just runs. 



*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 15/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
