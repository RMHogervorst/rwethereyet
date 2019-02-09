---
title: Hiding parts of github markdown without javascript
author: Roel M. Hogervorst
date: '2019-02-09'
slug: code-folding-github-markdown
categories:
  - github
tags:
  - codefold
  - hacks
  - snippet
  - html
---

This is something I have to search for a lot:

*How to hide parts of a github readme*

I use github exensively and even push analyses to github, so if you 
have a cool readme.Rmd and knit that to readme.md you sometimes end up
with huuuuuge codeparts that are not relevant for everybode, this code
snippet in pure html hides a part of your page.


Just add some html to a page.

```
<details> <summary> HERE TEXT SUCH AS CLICK ME </summary>

LOTS OF TEXT, OR CODE , SOMETHING ONLY USEFUL FOR INTERESTED PARTIES

</details>
```

Voila
