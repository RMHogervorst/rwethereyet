---
title: Schedule posts and netlify magic
author: Roel M. Hogervorst
date: '2019-02-21'
slug: schedule-posts-and-netlify-magic
categories:
  - blog
tags:
  - hacks
  - netlify
  - ifttt
  - webhooks
  - magic
difficulty:
  - intermediate
post-type:
  - walkthrough
---

This is a quick hack that I did not realize actually worked.

I often collect a lot of things and would like to spread them out over time.
So I schedule the posts on different dates. However, posts in the future are 
not yet build and if I don't push anything to this repo netlify will not
run the hugo process. I have a solution, but I first need some context:

This blog and the main one (See button above) are created from github - to
netlify to interwebs. 

- I write a post on my local computer 
- I push that file to my rwethereyet repo on github
- github tells netlify to download the repo when something is pushed
- netllify uses hugo to build the website for me
- netlify publishes the website

It is possible to manually trigger a rebuild of your website in netlify,
but there is also a possibility for other hooks to build your website.

- Go to netlify settings
- go to deploys
- build hooks

![like so](images/netlify_build_hook.png)

Use the unique url you get in a post request to rebuild your website.

Now comes the magic, although netlify tells us about Zapier hooks to deploy
your website, I don't have zapier. But I do have IFTTT. And IFTTT can do GET or
POST requests! 

I set up a IFTTT task: 

- IF: 3 days a week at 12 pm 
- THEN: webrequest to the URL from netlify (method POST, nothing in body and content type to text/plain)

This now triggers a new build, thrice a week so everything is fresh
