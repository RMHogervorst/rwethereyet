---
title: Components of My Smarthome
author: Roel M. Hogervorst
date: '2024-07-16'
slug: components-of-my-smarthome
description: An overview of devices I have and what I want to do in the future.
categories:
  - blog
tags:
  - smart-home
  - home-assistant
difficulty:
    - beginner
post-type:
  - post
---

This is an overview of my current smart-home and some future things I'd like to try.

Nothing here is sponsored. I get no money whatsoever from big domotica or anyone else.

## Brains
The brains of my smart-home are home-assistant. It just works, it is infinitely programmable, extensible and there is a huge and vibrant community. Everything connects directly to home-assistant or through a mqtt broker. Home assistant used to run on a raspberry pi, but the sd-cards wore out
and I didn't want to keep replacing them. Or maybe it was something else, but it
failed catastrophically multiple times over 3 years so I moved the installation 
from a backup to a container in kubernetes[^1] in my home server.
Home assistant uses a ZigBee plug that allows it to manage my ZigBee devices and
I put a esphome bluetooth accesspoint in the house that sends bluetooth information
to home assistant too. 

## Lights

Many people start with lights but I was super poor when I started so I have 4.5
lights that are programmable. One full color lifx light in a standing light in the living
room and a set of three full color pre-programmed esphome lights in my office.
There is also a smart plug that turns a string of lights on and off.

In the future I want to control living room lights in the ceiling with a shelly
but I haven't gotten around to it. I also want to add a wled light to the kitchen
but there is a connectivity issue there that I haven't solved yet.

## Audio and music

I have a collection of ripped dvds and cds and store them on a NAS. I play them
on my tv with kodi, and for streaming services I use a chromecast. When Google will
inevitably fuck this up and enshittify the chromecast I have to look for a
different solution for streaming.

In the future I will investigate music assistant with some small music players,
I have several raspberry pis lying around doing nothing so this is an ideal solution!

## Sensors

There are cheap bluetooth low energy (BLE) sensors that run about a year on a battery
and display the current temp. These things are not calibrated but you can reflash them 
with custom firmware (you can even turn them into ZigBee devices!) and you can
change the settings to recalibrate them to the current temperature. 

I have several plugs from athom.tech (pre-flashed esphome devices) that measure
electricity and can turn on or off. This measure thing is really useful for
determining if the washing machine or coffee machine are done! 

For turning things on and off you can also use ZigBee plugs from Ikea.

Speaking about Ikea, their window sensors are useful too! I have a few on windows
and doors that I sometimes forget to close.

I have a few sensors on the water and electricity devices, but I don't actually
do anything with that. If I had solar panels I could do more, but alas.

In the future I might make my dumb doorbell smarter by adding a sensor so I can 
flash lights when the doorbell rings. 

[^1]: You know what they say, if you have a problem and you solve it with kubernetes you have two problems. really it's fine, it works, I work with kubernetes at my $dayjob so I am okay. 
