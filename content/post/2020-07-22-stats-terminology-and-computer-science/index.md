---
title: Stats Terminology and Computer Science
author: Roel M. Hogervorst
date: '2020-07-22'
categories:
  - blog
tags:
  - 100DaysToOffload
  - data science
  - writing
difficulty:
  - advanced
post-type:
  - thoughts
  - clarification
slug: stats-terminology-and-computer-science
subtitle: "Words matter, terms too"
---

I am thinking about the meaning of specific terms and confusing things are for
new people in Data Science. 
I came into data science from psychology. Although psychology is quite statistics
heavy (for social sciences) and I did take an extra statistics elective, I never 
considered a statistics master program. I graduated in Medical Psychology. 
I felt miserable in a PhD program in Health Psychology and in a roundabout way 
I ended up in the methods and statistics department of Psychology.
After some time there I took a data-science traineeship and I took online courses
in data science. 

I also read a lot of data science writing. And boy are some terms confusing.

Things that are not understood the same:

- **Bias**: can mean intercept or bias node in neural network, but I only every thought of bias as: systematic deviation from the truth. The intercept or bias node can 
function like that, but not always. 

- Training set, **test set, (cross) validation set, assessment set**: Boy this can go 
wrong. Usually you split your data, and use one part to train your algorithm and
another part (test set) to see how it performs on data it has never seen before. But with
newer (like since the 90s) algorithms you want to check multiple times so you 
need to split another part of your data off to see how it performs and finally
check on data you have never seen before. How these chunks of data are called 
depends on who you ask. I have used *test* for the final-no-peeking-allowed part
and *validation* for the in between chunk of data. I have seen *analysis* for training set
and *assessment* or *holdout* too, but this is often used in cross validation 
procedure where we first split the data into *training* and *test*, leave test
for the end and split the *training* data into samples of *analyses* and *assessment*.

- **panel data**: means to me: data from a panel, like online survey or something. 
But has an econometric meaning too: a dataset with multiple measurements over 
time under a larger grouping. I would describe this last meaning as 
*multilevel* data, but I guess that only adds confusion.

- **independent and dependent /response variables**: I always immediately forget what is
what. I'd rather prefer to talk about X and y, or inputdata and labels. 

- **instrumental variables** : does not mean variables from an instrument. 
But variables that account for unexpected behavior between variables.


There are several ways of dealing with this confusion: You can write blogposts,
complain to people or sigh. But I think we cannot proscribe what people use,
there are rich traditions in social science, economy, math and computer science
that ended up using terms in their own way. I write it down into my knowledge 
notes and I try to ask questions and to simplify what I understand the issue to
be. 

Just keep asking questions about the most simple things. Let people explain 
their terms. You might catch yourself filling in wrong assumptions. And you
might learn new words!


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 19/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*

