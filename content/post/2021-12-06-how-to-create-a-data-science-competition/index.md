---
title: How to Create a Data Science Competition
author: Roel M. Hogervorst
date: '2021-12-06'
slug: how-to-create-a-data-science-competition
categories:
  - R
tags:
  - kaggle
  - python
  - flask
  - cocaine
  - NL
  - simulation
difficulty:
  - intermediate
post-type:
  - walkthrough
---

We recently hosted a small kaggle-like competition at work,
it was very specific for the the Netherlands: find the cocaine in seacontainers
that come into the port of Rotterdam. 
I was inspired by kaggle competitions that we did at Xomnia when I did my traineeship there. 
I find the goal of most kaggle-like competitions unrealistic for actual data science work, business people rarely want a super accurate model, they care about savings, costs and improved timings.
So in this case I don't judge people on how accurate they were, I judge them on how many kilos they found. This is highly unfair (also because I randomly generated those without relation to features) but is in practice what happens.
I'll talk about some technical details 
later but first: I made a starterset in python and R so my coworkers could 
start right away. 


## Creating a starter (code scaffolding)
This is super important! Although most actual data science 
work takes a lot of time, in these competitions you want to get to a submission
as fast as possible. The goal of these competitions is to improve your 
feature engineering and model choices and for that you don't want to spend a lot
of time on making sure your submission works.

So I created a complete starter for R and did what I could in the time I had for
python. A good starter has (in my opinion) codesteps that:

* read in trainingset
* some information about the dataset
* split into training and validation set (temporary test set)
* show one example of feature engineering
* train a model
* validate against validation set with metrics
* inspect predictions
* predict on testset
* create submission format

The zipfile I created also contained the trainingset, and testset
and a README that tells the story about the data.

I think this is called scaffolding in Education Science, you create the scaffolds
so people can build (and learn) faster.


## The data generation

My girlfriend thought it would be interesting to do predictions on containers.
Get into the role of Port Authorities / Custums and figure out how we could catch
the containers with cocaine hidden in it.

Of course there is no such dataset, it is by nature hidden. Cocaine smugglers
don't want to you to know what methods they use. And I don't think the Authorities would share data they have with me, if they have anything like this at all.

So I simulated it based on some public numbers: number of containers per year, types of load, countries of origin. 

First some facts:

* in October 2021 the Authorities in the Netherlands said they found at least 62.000 kg of cocaine
* There are approximately 4 million containers per year coming in at the port of Rotterdam
* 0.5% of containers are ever put into a scanner
* I learned that the cocaine is put into containers at their origin and there are people getting it out of containers at the harbor, before containers are transported out of the harbor. These people break into the area, know which container they need, break that container open and get the cocaine out and walk away.

Some assumptions:
* A man cannot carry more than 10 kilogram (you also have to take your breaking in tools, and you have to walk quite a bit).
* Criminals don't trust each other and don't work in large groups
* So I figured per container somewhere between 2kg and 40 kg (something that can be carried by between 1  and 4 people).

Some loose factoids I picked up by reading reports about cocaine smuggling:
* containers with products that transpire quickly (fruit, bananas, vegetables) are more popular for smuggling because there is more time pressure to get them through.
* Cocaine is produced in South America (and so containers from there should have a slightly higher probability)


My thought was like this:
* create basic dataframe with container information (cargo, date, weight, country of origin, ship, etc)
* Set a base probability for a container containing cocaine of mean 0.003 (this is higher than what I found in literature) (so normal distribution around that number)
* use modifiers to increase probabilies for containers coming from specific countries, during certain months, during some days, if they stopped during their
transit etc.
* multiply the base prob with the multiplyers 
* use that final probability for a random throw of yes or no cocaine.

If you make sure the modifyers are on average 1 the basic probabilies remain the same. (I allowed it to rise slightly).

[link to generators](https://github.com/RMHogervorst/cokehaven_generators)


## The scoring application

I generated a application that scores your submissions in python (flask)
[_link to flaskapp repository_](https://github.com/RMHogervorst/cokehaven_flaskapp)
I could have done that in shiny too, but I've been working with flask a lot lately and so I was quite comfortable with this.

About 0.5% of containers is scanned yearly and I gave the contestants 40.000 containers split into a trainingset (80%) and a testset (20%).
They could submit 400 of the 80000 containers in their testset. 'Give me the ones you think are highest probability of containing cocaine.'
This is how such a model would be used in practice so it made sense to me to score them in that way too.


The flask application has two pages: 
* a live scoring board that talks to the SQLite backend and retrieves the highest  200 scores in order (SQL query)
* a submission form where you upload a csv with your teamname

The scoring code uses pandas (i could have use polars too, but this was fast enough) to read in the csv, merge with the actuals inside the application, sum the kilos, calculate streetworth (every kilo is 50.000 euro) and write those things to the database. 

The application is baked into a docker container and uploaded to a cloud service.
I hosted the application on Azure (but any docker image hosting would do).

There are some issues of course, if the app crashes, you lose all scores because
the sqlite backend is inside the docker image, I thought that wouldn't happen in once day, but it actually restarted within 2 days. So you could write to a permanent database hosted somewhere else. That would be relatively easy to do.

All in all, I really liked building this, and the participants enjoyed it too!
