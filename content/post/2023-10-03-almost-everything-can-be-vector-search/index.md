---
title: Almost Everything can be Vector Search
author: Roel M. Hogervorst
date: '2023-10-03'
slug: almost-everything-can-be-vector-search
categories:
  - blog
tags:
  - 100DaysToOffload
  - podcastepisode
subtitle: ''
difficulty:
  - intermediate
post-type:
  - post
---
I listened to [Data engineering podcast -'real time vector search'](https://www.dataengineeringpodcast.com/real-time-vector-search-episode-393)

The interviewee is a vendor, but nevertheless the talk about vector databases was
interesting and not a pitch for rocksetdb. 

They talked about vectors, as they are used in ML (machine learning), for instance in embeddings and large language models.
Vectors are a numerical representation of something, with the idea that they live in a more semantic space. points in that space that are closer together are semantically more similar. But technically it is a an fixed size array for every row in your table. 

Some ideas I wanted to highlight:

- At some level many machine learning solutions are vector search problems (or you can turn them into one): finding the nearest neighbor, recommendations. 
- You can translate many types unstructured data into a vector space
- describing and translating a problem (into vector space problems) is a core part of data science solutions. 
- You probably don't need a special database for vector search, see it as just another column (with special properties) in your table. 
- vector data and vector search work better for OLAP (online analytical processing) databases.
- managing the lifecycle of vectors, (adding new ones, updating, deleting) is a data engineering problem; you're maintaining a data base or data warehouse. 


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 16/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
