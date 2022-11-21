---
title: Aggregating all My Tags over all My Websites
author: Roel M. Hogervorst
date: '2022-11-21'
slug: aggregating-all-my-tags-over-all-my-websites
categories:
  - blog
tags:
  - knowledge
  - knowledge-graph
  - taxonomy
  - inspiration
difficulty:
  - advanced
post-type:
  - walkthrough
subtitle: ''
---

What if I could link all my blogposts together into one browsable page?
That is what I've attempted to do with my new project. 

All my blogposts at <https://blog.rmhogervorst.nl> and <https://notes.rmhogervorst.nl> have tags. And since yesterday they all have a difficulty level too. 

I'm using hugo to create the pages for both sites, and I've build up a set of 
taxonomies (as they call it in hugo parlance)

```toml
[taxonomies]
   category = 'categories'
   tag = 'tags'
   post-type = 'post-type'
   difficulty = 'difficulty'
```

Every post has tags, a post-type and a difficulty.
Difficulties are one of beginner, intermediate or advanced and 
blogtypes are restricted to:

  - post (if I don't know)
  - clarification (you know how to do it in one language, how do you do it in another language)
  - tutorial (a step by step tutorial of how to do something)
  - walkthrough (a more loose version that you might not be able to follow)
  - link (mainly linking to another resource)
  - thoughts (what I was thinking)
  - analysis (analysis of data problem)
  - lessons-learned (I messed something up at in the past and I now understand why, and what someone else needs to know if they have the same issue: _that someone else is very probably me in the future_)


Tags are more free but fit into the larger network that I set up in kg.rmhogervorst.nl


## from tags to knowledge
Hugo makes the decision that tags are flat, there are no hierarchies. so to add that 
I either have to hack the tagging system or build something on top. So I did the last thing. 

Ultimately all the blogposts (and maybe a link blog too) should fit into the larger network of knowledge
and I want to be able to traverse the graph to find articles that are related.

So how do you build a network?
I chose to create a dataframe of nodes and a dataframe of edges that combine into
a network. 

nodes have an name, description, and a list of external links.
here is the top of the nodes data.frame in R:

```r
#library(tibble)
nodes <- tibble::tribble(
  ~name, ~description, ~external_links,
  "Data Structures", "High level topic from computer science", list(wikidata="Q175263"),
  "Graph","A data structure for networks", list(wikidata="Q2479726"),
  "dataframe", "Structure to represent two-dimensional tabular data with labeled axes (rows and columns)", list(wikidata="Q107420052"),
  "R", "the R language", list(wikidata="Q206904"),
  "Go", "",list(),
  "Bash", "",list(),
  'Python', "the Python language", list()
  )
```

And here are the edges:

```r
edges <- tibble::tribble(
  # subject, predicate, object
  ~from, ~relation, ~to,
  "XGboost","skos:narrower", "Boosted Tree Models",
  "LightGBM","skos:narrower", "Boosted Tree Models",
  "Catboost", "skos:narrower", "Boosted Tree Models",
  "Graph", "skos:inScheme", "Data Structures",
  "dataframe", "skos:inScheme", "Data Structures"
)  
```

I made the system a bit more complicated then absolutely necessary (breaking YAGNI):
- many nodes have wikidata links (But not yet a usecase for them)
- the relationships in edges are often done with The Simple Knowledge Organization System (SKOS) which could be useful in the future
- I've created nodes for all packages that I've used as tags

I can do this very easily with blogposts because both the notes and blog webpages export a json export of all posts too (I use that for local search).

## Future
For now my idea is to use D3 to visualise the network and I want to be able to
select all blogposts at distance 3 or something based on the network selection.

I'm excited by this project because just revisiting the blogs and tagnetwork inspired me for a number of new blogpost ideas!


### Links
- [blog.rmhogervorst.nl](https://blog.rmhogervorst.nl)
- [notes.rmhogervorst.nl](https://notes.rmhogervorst.nl)
- [kg.rmhogervorst.nl](https://kg.rmhogervorst.nl)
