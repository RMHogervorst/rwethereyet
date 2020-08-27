---
title: Upgrading Dependencies on My Blog
author: Roel M. Hogervorst
date: '2020-08-27'
slug: upgrading-dependencies-on-my-blog
categories:
  - other
tags:
  - hugo
  - 100DaysToOffload
subtitle: 'templating, complicated but very useful!'
---
My main [blog](https://blog.rmhogervorst.nl) had an annoying thingy, I had cool links at the bottom of every page to all my social media, but the icons would not show. I figured out the problem was with my theme. I'm using hugo to build the blog. That means it is a static site that is generated on every new push to the repo. 

`github-> netlify -> publish`

Hugo works very fast but the theme I use hasn't been updated in over a year
and the theme is using old versions of jquery, fontawesome (the core of my problem), bootstrap and katex. 

Luckily I don't have to wait until all 23 open pull requests and 60something issues are fixed. I can fork and implement them myself, or
I can make use of hugo's "smart" templating. which is what I did.

Now this is a rabbit hole but I'm writing it down so I can find it again later.

general main structure of the blog

```
.github/
.gitignore
archetypes/         [1]
config.toml         [2]
content/            [3]
data/
layouts/            [4]
netlify.toml        [5]
resources/
static/             [6]
themes/             [7]
```

1. Contains prepopulated template blogposts
2. Settings for blog
3. Where I place the blogposts
4. Contains page elements (404.html, footer, head, header)
5. Settings for netlify
6. Some fixed things like datasets, CSP rules for netlify and some images
7. The theme. 

The cool think about hugo is that you can import a theme (by placing it in
the theme folder) and that theme contains all the styling for all the pages. But if you want something different you can create a copy of the file in your local file structure and modify that copy. That copy is then used in the build of your website in stead of the version from the theme. 

That way you can use the theme as submodule and update it while keeping your version separate. For example in 
`/themes/beautifulhugo/` (the name of the theme is beautifulhugo) the file structure is:

```
.gitattributes      [1]
.gitignore          [2]
archetypes/         [3]
data/
exampleSite/
i18n/               [4]
images/
layouts/            [5]
LICENCE
static/             [6]
theme.toml
```

As you can see the folder structure is similar to my main structure.
So in a build the theme is taken as base, and the blog itself is overlayed on top of that. 


**Back to my problem**. bootstrap, fontawesome and katex are set in `themes/beautifulhugo/layouts/partials/head.html`

So in stead of waiting for the update from beautifulhugo, I copied the head.html from the theme to `layouts/partials/head.html` and modified that file (for some reason it is also defined in the footer.html, so I copied and modified that file too) to use the newest version of the dependencies. 

So now my logos are showing up again and I'm using the newest versions of everything.


*I’m publishing this as part of 100 Days To Offload. You can join in yourself by visiting https://100daystooffload.com, post - 33/100*

*Find other posts tagged  [#100DaysToOffload here](https://notes.rmhogervorst.nl/tags/100DaysToOffload/)*
