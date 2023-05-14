---
title: Logging Agent vs Handler
author: Roel M. Hogervorst
date: '2023-05-15'
slug: logging-agent-vs-handler
categories:
  - blog
tags:
  - 100DaysToOffload
  - logging
  - data-engineering
subtitle: ''
difficulty:
  - advanced
post-type:
  - post
---

If you deploy an application
and you want the logs to go to a centralized place
you have to make the logs go there from the machine where the system runs.

There are several approaches

- Add a handler to your logsystem that sends the logs to your central system.
- Add an agent that runs next to your main program on the same system that takes 
care of the sending of logs.

Whichever you choose depends on the trade-off you want to make (_all engineering is balancing trade-offs_). 

## using an agent
An agent can run as a deamon on a machine, or as a separate container in a pod.
You as a developer have simple application code that only needs to send logs to
disk (container case) or to a process. (you don't further care about it).
There is a clear separation of responsibility: your program only creates logs,
the agent makes sure the logs end up in the right place. It is easy to test, you can mock the agent. If your configuration for the agent is done right, you can use that same 
configuration everywhere.

An agent does require more resources and your deployment becomes a but more difficult.
Creating agents inside docker containers is a big nono, and adding a agent container in a side-car configuration in kubernetes is slightly more involved.

## using a handler
A handler is also a separation of responsibility, (that specific part of the program takes care of the logsending). Adding a handler to your program does not make your deployment
more complex. Adding this to one pod will cost you slightly less resources. 

However you have to extensively test your handler, does it send logs correctly,
do the threads work as intended, etc? Testing your code with a handler is more
annoying, you have to mock or swap out the handler. 


## Handling the trade-offs
For smaller numbers of deployments the added deployment complexity of agents 
can be too much. You can also use your resources slightly more efficiently.

For more deployments the trade-off can start to move towards agents. 

 
 
This [issue in the python-elasticsearch repositoy](https://github.com/cmanaha/python-elasticsearch-logger/issues/44) gives a few other reasons for using one or the other. 


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 7/100 2023*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
