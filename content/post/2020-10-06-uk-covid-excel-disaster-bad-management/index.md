---
title: 'UK COVID Excel Disaster: Bad Management'
author: Roel M. Hogervorst
date: '2020-10-06'
slug: uk-covid-excel-disaster-bad-management
categories:
  - thoughts
tags:
  - excel
  - 100DaysToOffload
  - COVID19
  - Coronavirus
subtitle: ''
---

So yesterday there was big news, according to the BBC there was a
failure to account for 16.000 COVID cases because of an IT-error.
What was the error? They used microsoft excel somewhere and than
saved the files as `.xls` files. But these files have a limit of  
65.000 rows.

> And since each test result created several rows of data, in practice it meant that each template was limited to about 1,400 cases. [2]

There was a twitter storm from people complaining about this in the following points

- excel was never designed as a database (although many people use it like that)
- this `.xls` format is superold and a newer one shouldn't have this problem (kind of misses the point)
- any idiot knows you need a database for this


And I get it. It seems insane that a governmental agency uses excel in
their pipeline! But this is the reality for many companies, people use excel everywhere. There are a bazillion critical business processes that run through excel. The tool was never designed for that usecase, but it works good enough apparently. 

Lets talk about the data pipeline for a bit (from the BBC article [2]):

> The issue was caused by the way the agency brought together logs produced by commercial firms paid to analyse swab tests of the public, to discover who has the virus.

> They filed their results in the form of text-based lists - known as CSV files - without issue.

> PHE had set up an automatic process to pull this data together into Excel templates so that it could then be uploaded to a central system and made available to the NHS Test and Trace team, as well as other government computer dashboards.

- Commercial firms do their analyses and send the results as `.csv` files.
- PHE pulls these csv's into an excel template
- PHE uploads data into NHS test and trace team.
- PHE uploads data into other governmental dashboards

The critical part is that Microsoft Excel is part of the pipeline. 

Reading in between the lines, we see that excel is used to :

- load the data
- transform / tabulate data
- store the data

It hides a lot of complexity and it also doesn't give feedback.

How did such a thing come to be?

![](valentin-petkov-uKS_wcTAMZU-unsplash.jpg)


### Cause 1: a proof of concept in production
I'm speculating here, but it could very well be that this is just a copy
of a pipeline for other infectious diseases, diseases that do not affect
thousands of cases every day. It is a glued together Proof of Concept
that never became a serious IT project. And now it is being repurposed
for a project it is absolutely not meant for.

### Cause 2: Shadow IT
In universities there are many small projects; important research, on real people, that are being kept in excel sheets. Because that is all these people know! They just don't know better and don't get the support
they actually need. 

Teaching researchers basic computer skills (like the non-profit software carpentry tries to do) was too expensive, deemed unnecessary, or
ignored. And now researchers are crying because their excel sheet was overwritten or genes are encoded to dates. People do these things because they use only the tools they know. If you don't support them they will
hack something together to get the work done. 

In corporations the same things happen. There are billions of small hacked together procedures that work until
the next software update breaks everything. This is the reality for organizations all over the world.

## Conclusion: CovidExcelGate is a failure of management
We should not focus so much on PHE's use of excel in their pipeline.
I believe this is a symptom of a much larger issues! How can you do such
a massive important job for the government and have no insight in your own processes? 
This is a failure of management. Someone should have talked with all the stakeholders and figured out all the steps that were taken. But nobody did. 

- Where was the IT support team? 
- Where was the data architect?
- Who had the overview?

This is why top people get the big salaries, take responsibility for the organization. So if I was the Department of Health and Social Care, I would look at the organogram of PHE [3], and call in the Chief Executive (Duncan Selbie), maybe the director of corporate affairs (Alex Sienkiewicz). Let them explain how a shadow IT came to be, or where the IT support was for their massive job.



### Links

- [ [1]BBC: Covid: 16,000 coronavirus cases missed in daily figures after IT error](https://www.bbc.com/news/uk-54412581)
- [ [2] BBC: background on specifically excel](https://www.bbc.com/news/technology-54423988)
- [[3] leadership organogram of PHE (note that there is no technical Officer anywhere in this organogram!) ](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/903185/Our_Leadership_organogram_22_7_2020.pdf)
- [shadow IT description on wikipedia](https://en.wikipedia.org/wiki/Shadow_IT)
- <span>Photo by <a href="https://unsplash.com/@thefreak1337?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Valentin Petkov</a> on <a href="https://unsplash.com/s/photos/ducktape?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 35/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
