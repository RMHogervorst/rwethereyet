---
title: What is a Footgun?
author: Roel M. Hogervorst
date: '2022-11-21'
slug: what-is-a-footgun
categories:
  - blog
tags:
  - design
  - software
  - human error
difficulty:
  - beginner
post-type:
  - thoughts
---

I call some things 'footguns'. What do I mean with that?
A footgun is a gun that is designed to shoot yourself in the foot.
I don't know anything about guns, I have no use for them. But I've heard about this phrase
and the idea stuck:

> A footgun is a piece of code that is designed to do the wrong thing easily.

It is superhard to do the right, safe thing, and easy to do the wrong thing.

It is actually a case of bad design, and more often bad defaults.

![a child shooting a water pistol](michael-starkie-WhAZTTt7Lcw-unsplash.jpg)


Examples: 

- openssl (a cryptographic library) had default settings for many algorithms that made it unsafe in use. You had to choose specific settings to make it safe. 
- During WW2 certain bomber airplanes crashed often on landing. Research found out that the levers for the landing gear were close to, and felt and looked identical to flaps control. So when pilots tried to lower the landing gear, they changed configuration of the wings and it dropped out of the sky.
- in R when you use a data.frame and select columns, if there is only one column remaining you get a vector back, and not a data.frame. This can lead to many problems. {tibbles} do no such thing, you will always get data.frames back.


So, when you do find footguns in your code, please please remove them and create a pit of success for your users:

> Make it easy to do the right thing and make it hard to do the wrong thing.



## Links
- [wictionary definition of 'footgun'](https://en.wiktionary.org/wiki/footgun)
- [urban dictionary definition of 'footgun'](https://www.urbandictionary.com/define.php?term=footgun)
- Photo by <a href="https://unsplash.com/@starkie_pics?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Michael Starkie</a> on <a href="https://unsplash.com/s/photos/water-pistol?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
