---
title: Squeezebox with Music Assistant Works Really Nice
author: Roel M. Hogervorst
date: '2025-03-03'
slug: squeezebox-with-music-assistant-works-really-nice
categories:
  - blog
tags:
  - music
  - music-assistant
  - rpi
difficulty:
  - intermediate
post-type:
  - post
subtitle: 'slimproto'
---

Man squeezebox (slimproto)[^4] is really good! 
I have a rpi2 that I installed picoreplayer on, it is a small program that can play music over the speakers[^5]. 
It is great, I have several pis lying around that I do not use anymore[^1], and this is a good way to use them.

When I send a command to play music with music assistant the rpi starts playing within a second. 
I also have a few Sonos speakers and they take almost twice as long to play music. 

Music assistant is a really nice project, it plays[^2] from my spotify and all 
the cd's I ripped over the years. And it plays it over all sorts of speakers[^3], 
and it integrates with home-assistant.

I now have several automations that play music when I want over the speakers I want.

home assistant with music assistant makes useful and silly things possible:

- Play the imperial march (star wars) when your father-in-law enters the house? possible
- Turn on christmas music and turn on the christmas tree with one button? possible
- Play band-aid on all speakers and deliver world peace? seems to be broken at the moment


[^1]: I loved the raspberry pi's when they came out, but they are not super reliable over years. There were random crashes, sd card failures etc. 
[^2]: It plays from local files, internet radio, apple music, deezer, soundcloud, spotify, plex, siriusxm, subsonic, youtube music [and more](https://www.music-assistant.io/music-providers/). But I don't have all of those services. 
[^3]: It plays over airplay, DNLA, google cast, slimproto, sonos [and more](https://www.music-assistant.io/player-support/)
[^4]: I don't really know, or care really, but there are many names for this thing , it is called **squeezelite**, I think the device is called **squeezebox**, the protocol is called **slimproto**. 
[^5]: The pi runs [piCorePlayer](https://www.picoreplayer.org/), it uses slimproto (a streaming protocol for music).
