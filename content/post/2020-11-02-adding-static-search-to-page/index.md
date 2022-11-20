---
title: Adding Static Search to Page
author: Roel M. Hogervorst
date: '2020-11-02'
slug: adding-static-search-to-page
categories:
  - blog
tags:
  - 100DaysToOffload
  - search
  - javascript
  - hugo
difficulty:
  - intermediate
post-type:
  - thoughts
---

![a loupe on a macbook, because why not](agence-olloweb-d9ILr-dbEdg-unsplash.jpg)

I just added static search to this website, and it is super easy. (see [/search](https://notes.rmhogervorst.nl/search) )

### How does it work?
* we create one big json with all the page content (index.json).

Every page is summarized into title, summary, content and tags. 

* The search javascript goes through this.

The logic in that javascript matches the keywords against the content of the pages. You can even modify the relative weights of the search parts.

### How can I add it too?
I followed the guidance here: [on the hugo discourse website](https://discourse.gohugo.io/t/a-simple-javascript-based-full-text-search-function/29119).
Add the following things to the website:

* a shortcode in [layouts/shortcodes/search.html](https://github.com/RMHogervorst/rwethereyet/tree/master/layouts/shortcodes/search.html)
* a custom javascript in [static/js/search.js ](https://github.com/RMHogervorst/rwethereyet/tree/master/static/js/search.js)
* a page for search: [content/search.md](https://github.com/RMHogervorst/rwethereyet/tree/master/content/search.md)
* a custom layout that creates a json in [layouts/index.json](https://github.com/RMHogervorst/rwethereyet/tree/master/layouts/index.json)
* Modify the config.toml to also produce json for the main page:
```
[outputs]
   home = [ "HTML", "JSON" ]
```

I tried it out and it worked out of the box! The only thing
I modified was the search.html shortcode because it used German words for AND / OR search.


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 38/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*

[Image from unsplash by Agence Olloweb](https://unsplash.com/photos/d9ILr-dbEdg)
