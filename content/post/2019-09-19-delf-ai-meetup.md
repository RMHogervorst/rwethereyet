---
title: Delft AI meetup AI for Intelligent Vehicles
author: Roel M. Hogervorst
date: '2019-09-19'
slug: delft-ai-meetup-ai-for-intelligent-vehicles
categories:
  - blog
tags:
  - data science
  - ADAS
  - autonomous cars
  - AI
  - inspiration
difficulty:
    - beginner
    - intermediate
    - advanced
post-type:
    - thoughts
---

I was at the [Delft Ai meetup](https://www.meetup.com/delft-ai-meetup
) an initiative of the Computer science department
of [TU delft](ai.tudelft.nl). These meetings combine a talk from someone from
industry and an academic.


There were 2 speakers, Bram Bakker from [Cygnify bv](https://www.cygnify-solutions.com/) and [Dariu Gavrila](http://gavrila.net/), professor
at TU Delft.

## Bram Bakker Cygnify Bv : The disruption of driving
phd reinforcement learning Leiden.

SOME DEFINITIONS
autonomous driving, andvanced driver assistnace systems (AD/ADAS)
(Cygnify zitten in Leiden, outside perception and inside driver monitonr)
are hiring.

SELF DRIVING CARS ARE COMING IT SEEMS, WHAT IS POWERING DEVELOPMENT
what is powering development:
- sensors: lidar, radar, cameras
- high def digital maps (tomtom doet hier veel denk)
- computing power  (both in vehicle, and off board for simulations, model training)
- AI algorightms deep learning based perception, tracking, prediction models.

SINCE I AM BUILDING AND DESIGNING SYSTEMS AT MY WORK I AM INTERESTED IN
HOW MACHINE LEARNING IS USED IN PRACTICE. THIS IS REALLY PRACTICE.
AS ALWAYS THE ML IS A SMALL PART OF THE MACHINE.
SENSORS ARE CONNECTED TO A BIG CHUNK OF PERCEPTION.
- DETECTING WHERE YOU ARE
- DETECTING WHO ELSE IS THERE
- POSSIBLY ESTIMING / FORECASTING WHAT OTHERS ARE GOING TO DO.
CONNECTED TO PLANNING
CONNECTED TO ACTUAL CONTROLS: GAS PEDAL, BRAKE ETC.
architecture is quite interesting. revolution mostly in perception part.
- sensors connected to perception to planning that influences control

levels of automation
currently at level 2 (driver must continuously monitor the system)
from level 3 on user doesn't need to monitor, except if prompted.
level 4 hands off, eyes off
level 5 full automation

I DID NOT KNOW THIS! 60 -90 % OF PEOPLE WITH DRIVING ASSISTANCE ON CURRENT CAR
DON'T WANT IT ON A NEW CAR.
current users of ADAS 23% annoying or bothersome
another 21% shut if off. 60-90% don't want it on next car
some fighting with it.

what are current problems

# Unexpected and rare things

- rare objecst on the road.
- unclear road markings,
- unpredictable behavior of other road users

(only works on data where we have trainings data)

# overreliance on system by humans

- when they shouldn't

# overbearing ADAS

- to triggerhappy (false negative reducement)
- ADAS does not take context into account

# HAVE TO MAKE A DECISION, THERE IS NO GRADUAL LEVELS
Let the human drive and support him / her
or let the car drive in certain conditionsand don't expect human take over.

HIS COMPANY FOCUS ON LEVEL 1/2 DRIVING WITH ASSISTANCE (THAT DOESN'T SUCK)
level 1/2, human drives, but system monitors outside and driver state
draws attention to important elements or hazards if it appaers the
with good hmi
emergency break only after attention is clearly not paid.

- estimate gaze.
- LOOK OUTSIDE AND estimate where driver looks.

want to do augmented reality HUD
- HUD displays on the windscreen in the same focal length as real thing SO THE WARNINGS AND BOXES ARE FOR YOU THE DRIVER ON THE OBJECT, AND NOT IN A SPERATE SCREEN
-

prediction of other users (forecast what is going ot do)

Social scene LSTM (look at one user, take other users into account and scene)
Alahi et al 2016, and SS-LSTM adds scne Xue et al 2018.
Multi modal social sciecne
(earlier work on pedestrians, this also other wheeled)
wheeled users are heavely constraint by road use map lane data
- learn first on trajectories data
- than on real data
- (than on bicycles )

separate: high level direction
and trajectory relaisatoin for thos directions

Complete system in let the driver drive but add assistance
-

---asdfa
THE NEXT TALK WAS BY
prof. dr. Dariu Gavrila TU self driving vehicles in the city

He talked about one of the biggest issues for self driving cars: non-cars. Pedestrians and cyclists are hard to predict. 
SELF DRIVING IS EASY ON THE HIGHWAY AND AMERICAN STREETS BECAUSE THEY ARE
BUILD FOR CARS. 

The main challenge: pedestirans cyclists VULNURABLE. 
- DYNAMIC AND CLUTTERD BACKGROUNDS
- PEDESTRIANS CAN EXHIBIT HIGHLY IRREGULAR MOTHION

HE HAD A BEAUTIFUL PICTURE OF DELFT WITH BICYCLES AND PEDESTRIANS THAT REALLY SHOWED HOW TIFFICULT IS WAS TO DETECT THEM. SO I HAVE TO 

![](/post/2019-09-19-delf-ai-meetup_files/01 Afternoon traffic in Amsterdam (Photo credit- Copenhagenize Design Co).jpg)

(ze hebben wel scientific programmers hier )

ALL ABOUT PREDICTING AND DEALING WITH Vulnarable ROAD USERS.

Vulnarable road users is difficutl for human drivers also for self driving cars.

Prediction for what road users will do. want adaptive driving style, safe comfortable and
time efficient.

systems components
- 3d environment recovery
- add labels
- time erelvanct things
-

need to compress the data
turn pixels into stixels stick shaped superpixel, with 3d position, sematnic class and id.
(cool sort of semantic class, car, car 1 car 2 etc.)


eurocity persons detection dataset eurocity-dataset.tudelft.nl (kwarter of million cost)
- persons, images, 31 cities in europe, 4 seasons, da night, accurate labels.
- echt mega!
- Pretty good performance

- more data and labeling would increase performance (no saturation yet)
- pre-training thi dataet on smaller sets does improve (domain transfer)
- bias geografic yes if they train on western europe worse on easter europe etc.


other things: fast pedestrian detection taking care of occlusion
probabily of pedestrian CROSSING (combination of camera with radar is faster )

intent recognition. predict if person will continue or stop
bayesian , states : contiue, stop, accelerate etc.
mixture of gausians

also with cyclists
dynamic bayesian network

predictions for head orientation, direction etc.

THERE WAS NOT A FOCUS ON AN COMPLETE SYSTEM, THESE ARE JUST PARTS THAT DO THINGS
USEFUL FOR SURE.



WHAT DID I LEARN:
- AUTONOMOUS DRIVING IN THE CITY IS DIFFICULT. USER EXPERIENCE IS VERY IMPORTANT:
OR USERS DON'T WANT IT, OR THE RIDE IS TERRIBLE. THERE WILL NOT BE A GRADUAL TAKE OVER
IN LEVELS. BECAUSE LEVELS 3/4 ARE HORRIBLE FOR USERS, THE SYSTEM DRIVES AND YOU HAVE TO
PAY ATTENTION, THIS COMBINES A MACINE WITH THE WORST OF HUMAN, CONSTANT VIGILANCE WHILE
NOT HAVING TO DO ANYTHING IS BAD!

ARCHITECTURES USED: neural networks: bayesian dynamic network, ltsm


* [this specific Meetup page](https://www.meetup.com/Delft-AI-Meetup/events/262891404/feedback/)
