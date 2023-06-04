---
title: Machine Learning is Imitation of Outputs
author: Roel M. Hogervorst
date: '2023-06-03'
slug: machine-learning-is-imitation-of-outputs
categories:
  - blog
tags:
  - AI
  - 100daystooffload
  - ml design
  - AI myths
subtitle: "just because your modeloutput looks good doesn't mean it is true"
difficulty:
  - advanced
post-type:
  - thoughts
---


I listened to a data skeptic episode 'Why machines will never Rule the World', an interview with Jobst Landgrebe and Barry Smith. I will probably butcher some
of their ideas and I haven't read their book yet, but I really like this idea:

> Machine learning imitates outputs

![an image of hand and its reflection in water](serrah-galos-H6xxqTIHOTM-unsplash.jpg)

ML is a mathematical model, a simplification of a complex system. But it is not 
really a simplification of that complex system, it is a imitation of the outputs.
Because all you put into a Machine Learning model is the inputs and the outputs.

The model then creates a function that turns input into outputs according to
historical data (training data). 


ML is not an approximation of the real world complex system, it is imitation of outputs. This works great when the complex system that ML tries to imitate is not too complex. 
But if you use ML to model complex decision processes, that involve motives and incentives that are not in the data, your model will not be great.

## ML systems are not copies of real world complex systems
If you use an ML-model to try to provide explanations about complex systems, you might be fooling yourself. There is no way to know if the mathematical representation in your model is the same or even similar to the actual system.

I think the bayesian and likelihood modeling techniques in science are better equiped to learn about the world. In those systems you first create theories and models of the world and then fit those to your data. By comparing models to your
data you can find more or less evidence for your theories. 

If you take a big dataset and put all the modeling decisions into the algorithm _(insert brrrrr deep learning goes brrrr meme here.)_ and then use that model
with explainable AI to figure out how the world works, you're doing it in the wrong order. 




## Refs
- [Data Skeptic episode 'Why Machines will never Rule the World'](https://dataskeptic.com/blog/episodes/2023/why-machines-will-never-rule-the-world)
- Photo by <a href="https://unsplash.com/@serrah?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Serrah Galos</a> on <a href="https://unsplash.com/photos/H6xxqTIHOTM?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 9/100 2023*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
