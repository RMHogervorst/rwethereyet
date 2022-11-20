---
title: Complexity in Data Science Operations
author: Roel M. Hogervorst
date: '2021-05-23'
slug: complexity-in-data-science-operations
draft: true
categories:
  - blog
tags:
  - platforms
  - complexity
  - Tesler's law
  - Machine learning
difficulty:
  - intermediate
post-type:
  - thoughts
---
HET LOOPT NIET ZO LEKKER. 
MISSCHIEN MEER FOCUS OP COMPLEXITY VAN ML DOEN? 

There are more and more companies that provide solutions to bringing ML into 
production. 

... Before I continue there is a conflict of interest here, I will talk about DataIku
and UbiOps. My $dayjob (Ordina) works with UbiOps and sells services around machine learning. Ordina also has a relation with DataIku. Although I don't directly
benefit from you using their services, I want to be open up front... 
Back to the story.

Bringing a solution to production can difficult. There is even 
a new field: MLops![1] Because ML is really difficult. The models are not 
that difficult, but translating a business problem [2] into a model and solution 
requires skill! I will not even talk about that part here! The other hard thing
is making sure your model is available, performance remains on
par and retrains when necessary! So let's talk about that
second part: 

> Bringing a model into production is really hard

And let's reword that

> Bringing a machine learning model into production is complex

I call it complex because we have to think about Tesler's law, or the 'Law of
conservation of Complexity': 'For any system there is a certain amount of complexity
that cannot be reduced'. When you reduce complexity on one side, there comes higher
complexity on the other side. And that is what I see happening too. 

Keep in mind that the business does not want an XGboost model. They want accurate
predictions of churn, or sales forecasts for the next week. Nobody cares how 
you do it. The business cares about the results you provide, so you need to 
connect the data that makes your model work and give back the predictions you create.
Your machine learning model is just a small part in a web of business processes. 
And the complex parts are very much the integrations. 

What are the components that go into a production machine learning model?

* data needs to be combined from multiple places
* data needs to be transformed so the model can handle it
* Ideally you monitor changes in input data
* You train a model on a (virtual) machine, using training data
* the end product of training is a trained model. That can be used to predict new cases
* the prediction cases need to go through the same transformation steps as the train data
* You need some way to check performance of the model
* you need to know if the training was complete/failure, how long it took etc.
* Scheduling: you need to retrain if performance is worsening, or just on a regular basis.

For many of these steps there might already be solutions in your company.

So let's talk about solutions that 'solve' your deployment of machine learning
models. I think they all hide a lot of complexity, which can be exactly what you need! 
But it can also bite you in the butt when you want to integrate the model into
your business.

So what are some options:

### Complete platforms, with a GUI.
Examples are DataIku, KNINE, RapidMiner. 
A complete platform with a visual interface where you connect components into a pipeline. 
Often provide a way in for python models from scikit learn (a well known python machinelearning package). I have some experience with DataIku and I think it is
great for building an entire pipeline:
connect to a database, retrieve data: clean it up, split it up, use a part to
train a model, the rest to validate your performance. push the trained model
to a special place to become an API that you can use externally or automate 
the workflow. 

The tuturials are great
but interfacing with your production systems still requires a lot of work.
It feels like a heavy solution for simple machine learning models but it does 
have automated logging! and you can roll back a model if you want to. And the
flow from experimentation to model is relatively smooth.

Not really clear if the platform will send you a message if the model starts 
misbehaving. For access control you have to more or less connect active directory
or something, or manually approve every person, which means a duplication of
control structures in the company. 

#### Where is the complexity
Making all the parts of the toolchain work together is really difficult, and
so DataIku eats it all. In essence you deliver data to the dataiku server (or 
let it retrieve it) and out comes a solution. 
This can make it difficult if you want to use other
tools in your company too. You cannot really make dataIku work with airflow to
run a job. I also don't know if  you can push all your logs to a central logging
location, of use your company's alerting system if something goes wrong. 



### More managed kubernetes solutions
A solution like UbiOps: More low level, they manage a kubernetes platform and 
containers for you, you take your python (or R) code and put it into special
functions. The platform takes care of turning it into containers and hosting it
as an API. 

KubeFlow has a similar thing but is open source, I have a feeling kubeflow is 
less polished (I haven't really worked with kubeflow much). 

#### Where is the complexity
Because UbiOps manages the containers, the builing process, scheduling etc you 
have less to say over this. Most standard things work, that is the great selling
point! But if you want to do advanced stuff, you still have to manually specify
which system dependencies you need, maybe specific python package versions etc.

Doing advanced stuff is possible, but in a way, you are taking over management
of the kubernetes cluster again. Exactly what you wanted to avoid by using this
solution.

### Going full on manual
Building your own python/R/Spark/Scala solutions. This is the most complex. But
it does give you full control over everything. But setting up everything yourself
requires:

* A central git repository
* A CI/CD pipeline
* Artefact store
* Starting (virtual) machines 
* installing everything
* scheduling runs
* sending logs and metrics to 
* metric, alerting and logging systems
* connecting to data sources 
* probably more that I forget


What it costs you is: time. You don't have the time to set this up, if your company
has most of the phases ready than we have a differnet story. You only need
to connect the parts that are not done yet. 

## Now what?
So you need to make decisions. These managed solutions cost a lot of money,
but they will save significant time. By standardizing components you take make 
more uniformity. But the development and maintainance of these components still
remains complex. 



[1]: MLops is like DevOps an concatenation of two words: Machine learning Operations (and devOps stands for development/ Operations). MLops is about practitioners not only building the machine learning model, but owning the lifecycle too, so also deploying, keeping track of performance etc.
[2]: Even though I talk about 'Business' problems, if you are not a business, it still works. It's very broad. Government agencies also use ML and have problems that we can call business problems.


## Notes and references
* I first read about Tesler's law in the FS blog. https://fs.blog/2020/10/why-life-cant-be-simpler/ 


