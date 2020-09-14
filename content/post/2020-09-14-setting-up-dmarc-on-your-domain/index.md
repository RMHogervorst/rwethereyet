---
title: Setting Up Dmarc on your Domain
author: Roel M. Hogervorst
date: '2020-09-14'
slug: setting-up-dmarc-on-your-domain
categories:
  - other
tags:
  - internet
  - knowledge
  - solution
  - DMARC
  - DNS
subtitle: ''
---

I received an email from hackbros1337 (hackbros leet; yes
that was their email adres) with a responsible disclosure of 
my domain. I believe the impact of their find is rather small but
I thank them anyways. So this post is just a small update on what I did after receiving their mail and for me when I forgot what it
was and how I solved it. 

I received their email on september 12th 2020 with the message:
'Invalid DMARC record leads to email spoofing'.

And 

>  fault : (No DMARC record)

and

> Impact
Spammers can forge the "From" address on email messages to make messages appear to come from someone in your domain. If spammers use your domain to send spam or junk email, your domain quality is negatively affected. People who get the forged emails can mark them as spam or junk, which can impact authentic messages sent from your domain.

I had to look up what that all means. But the main message is serious, if people send spam they can use whatever 'from' addres they want, there is no check whatsoever, so even though I currently do not have any email associated with this domain, spammer could use my domain for their messages: something like pharmacy@mydomain.com . This is bad for me, because people who
are duped will go to my websites and blame me. 

Because we all hate spam there is an email validation solution called [DMARC; Domain-based Message Authentication, Reporting and Conformance](https://en.wikipedia.org/wiki/DMARC "en.wikipedia link to DMARC"). Which I believe is used by the larger parties such as gmail and microsoft. 

In short, an email server that receives an email can authenticate the email against the 
DNS records of the domain. 

I used a guide from report-uri.com and added a TXT record to my DNS config for `_DMARC.domain`:

```
v=DMARC1; p=none; rua=mailto:report-uri-email-adress 
```

I could have used my own email address, but I don't expect a lot of traffic, none actually, and report-uri will compile nice reports for me.

I have set the p=none which does not prevent abuse, but if I
do receive a lot of problems I will change it.

*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 34/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
