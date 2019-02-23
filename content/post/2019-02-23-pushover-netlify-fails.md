---
title: Send a push notification with pushover when your netlify build fails
author: Roel M. Hogervorst
date: '2019-02-23'
slug: pushover-netlify-fails
categories:
  - other
tags:
  - netlify
  - pushover
  - ifttt
---

In [my previous post about netlify](https://notes.rmhogervorst.nl/post/2019/02/21/schedule-posts-and-netlify-magic/) I showed how you can automatically rebuild your hugo blog
with netlify through IFTTT. But there is also a reverse possibility:

> Send a notification when your blog deployment fails or succeeds.

Here's what we are going to do: let netlify send a message to a url that is picked up by IFTTT and let IFTTT send a message to pushover

### More details IFTTT

- activate IFTTT [webhooks](https://ifttt.com/services/maker_webhooks)
- go to the documentation of webhooks (this will show you the URL)
- it will show you your key and a link like: 'https://maker.ifttt.com/trigger/{event}/with/key/YOURKEYHERE'

The magic is in the '{event}' part, replace he {event} part with a good event_name

- we then make a listening event in the 'IF' part: 
![ifftt first part](/post/2019-02-23-pushover-netlify-fails_files/Screenshot_2019-02-23 IFTTT.png)
- add the notification part that you want in the 'THEN' part !['THAN' part](/post/2019-02-23-pushover-netlify-fails_files/Screenshot_2019-02-23 IFTTT(1).png)


Now we have to set up netlify

### More details about netlify setup
- go to your netlify 
- go to deploy setttings
- go to deploy notifications
- add a deploy notification / outgoing webhook
- fill in details 'event to listen to: deploy failed', 'URL to notify: the link you created with event_name filled in. 

Done
