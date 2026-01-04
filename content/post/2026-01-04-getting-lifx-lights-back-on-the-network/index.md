---
title: Getting Lifx Lights Back on the Network
author: Roel M. Hogervorst
date: '2026-01-04'
slug: getting-lifx-lights-back-on-the-network
categories:
  - blog
tags:
  - smart-home
subtitle: 'lifx original without an iphone'
---

I have an original lifx light. It worked fine without cloud connection, until a week ago.
LifX is a full spectrum rgb led light that connects through WiFi. This is awesome
because home-assistant can just control this light. However the light suddenly dropped of the Wifi.

There is a reset button on the light so I used that, but to get the light back on the network you have to use the lifx app, and also you have to make an account.
I hadn't used that app in years (thanks home-assistant!), so I had to install it on my android and to my surprise I got a cryptic message that my bulb was not compatible with android, please contact support.

I searched the lifx website and found no solutions for android. 
I contacted lifx support (told them I have computer and android, was there anyway to fix my light?) and got a fucking LLM that told me there was no way to do that.
I angrily ordered zigbee bulbs to replace this fucking piece of shit, but a few days later an actual human answered my requests and send me actual useful information.

## How to get your lifx lights (original) back on your wifi (without the lifx app)

There is a tool to onboard the device again with your laptop. 
It even works on linux (if you are okay with running a random binary from the internet) 
The tool requires your wifi credentials, and serial number of the device.

Since I couldn't find that information on their website, and web search will now just make stuff up, I'll just copy the relevant info here for others to find:

- Windows Download:  
[https://hosted.lifx.co/onboarder/original_setup%20windows.zip](https://hosted.lifx.co/onboarder/original_setup%20windows.zip)  
- Linux Download:  [https://hosted.lifx.co/onboarder/original_setup%20linux.zip](https://hosted.lifx.co/onboarder/original_setup%20linux.zip)  
- Mac Download (Apple Chip):  [https://hosted.lifx.co/onboarder/original_setup%20mac.zip](https://hosted.lifx.co/onboarder/original_setup%20mac.zip)   
- Mac Download (Intel Chip):  [https://hosted.lifx.co/onboarder/original_setup%20mac%20intel.zip](https://hosted.lifx.co/onboarder/original_setup%20mac%20intel.zip))


I think in the future I only want esphome devices on the wifi and all other devices must be zigbee, or matter.
