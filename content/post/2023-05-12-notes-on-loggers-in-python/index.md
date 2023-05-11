---
title: Notes on Loggers in Python
author: Roel M. Hogervorst
date: '2023-05-12'
slug: notes-on-loggers-in-python
categories:
  - blog
tags:
  - 100DaysToOffload
  - logging
  - python
subtitle: 'Because I have to look it up once in a while'
difficulty:
  - intermediate
post-type:
  - post
---

Python loggers are very versatile but debugging what goes wrong is annoying.
Here are a few things I learned or have to look up all the time.
(I guess this works for any logging system, not just python, but I've only worked
with python and the R [{logger}](https://cran.r-project.org/web/packages/logger/index.html) package)


## Terms
(from [docs.python.org](https://docs.python.org/3/howto/logging.html#))
- **loggers** expose interface that applications use
- **handlers** send to appropriate location
- **filters** determine which log records to output
- **formatters** specify layout of log records in final output


## Loggers are hierarchical
You call a logger by name with logging.getlogger(name).

Loggers have hierarchical namespace, which is a fancy way to say that
the ordering goes like this:
if you don't specify a logger name (f.i.`logging.info()`), you call the root logger.
If you use logger `name.name` the logger above is called `name`.


```bash
rootlogger
    |
 name-logger
    |
 name.name-logger
```

Convention is to use the filename for the logger, since you usually order your 
modules in an hierarchical way. you call that logger like so:

`logger = logging.getLogger(__name__)`


Why does this matter?
If a logger has no handler defined, it looks in the logger above. 

So if you define a handler for `name` all the underlying loggers (`name.baz`, `name.name`) (in namespace terms)
will use that one as well. 
Loggers default to propagate too. This leads to interesting situations:

- if you specify a handler for the rootlogger
- and specify a different handler for logger `name`
- messages from `name` end up in both the rootlog handler and the `name` handler


## Log records
<https://docs.python.org/3/library/logging.html#logrecord-objects>

Log records have as most important components:
- level (an integer (10=debug, 20=INFO))
- name (name of the logger)
- msg: actual message
- exc_info (a tuple with exception information)
- created (when the record was created )

But you can add extra information in log records.
The dagster logging records contain a component dagster_meta, that component is a huge dictionary of all the relevant information for a dagster run. 

## Stopping certain messages from getting into your logs
- filter out specific log messages by a specific filter
- changing the logging threshold of a logger
- changing the generic logging threshold


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 5/100 2023*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
