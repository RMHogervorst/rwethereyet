---
title: Making Json Endpoints for My Websites
author: Roel M. Hogervorst
date: '2023-03-04'
slug: making-json-endpoints-for-my-websites
categories:
  - blog
tags:
  - data-engineering
  - usability
  - Hugo
difficulty:
  - intermediate
post-type:
  - post
subtitle: 'json layouts are pretty easy'
---
What if you want to do something with your blogposts? You could go and parse all
the markdown, or scrape the webpages. Or, you could generate the content into machine-parsable format as well. 

I've added json 'endpoints' to all of my static websites.
That is useful for me if I want to process that data later and it doesn't cost
me anything.
You can also use it for search on the webpage (though I don't use that so much)

## How
All my static websites are created with hugo. Hugo build pages really fast
and rebuilds them on changes. 

So how did I do it?
I looked online and found several examples (can't find them anymore).
But basically:
- tell hugo you want json output too
- create a template for hugo to create


in config.toml tell Hugo you want json output too:

```toml
[...]
[outputs]
   home = [ "HTML", "JSON" ]
[...]
```

In layouts/ add a index.json, this is the index.json for 
this blog (notes.rmhogervorst.nl):

```json
[ {{- $i := 0 -}}
{{- range where .Site.RegularPages "Section" "ne" "" -}}
   {{- if not .Params.noSearch -}}
      {{- if gt $i 0 }},{{ end -}}
      {"date":"{{ .Date.Unix }}", "url":"{{ .Permalink }}", "title":{{ .Title | jsonify  }}, "summary":{{ with .Description}}{{ . | plainify | jsonify }}{{ else }}{{ .Summary | plainify | jsonify }}{{ end }}, "content":{{ .Content | plainify | jsonify }},"tags":[ {{- $t := 0 }}{{- range .Param "tags" -}}{{ if gt $t 0 }},{{ end }}{{ . | jsonify }}{{ $t = add $t 1 }}{{ end -}} ], "level":[ {{- $t := 0 }}{{- range .Param "difficulties" -}}{{ if gt $t 0 }},{{ end }}{{ . | jsonify }}{{ $t = add $t 1 }}{{ end -}} ] }
      {{- $i = add $i 1 -}}
   {{- end -}}
{{- end -}} ]
```

Because this is awful to read let's explain it so I can revisit this later.

- `{{- range where .Site.RegularPages "Section" "ne" "" -}}` only regularpages (not category pages etc.)
- `{{- if not .Params.noSearch -}}` this allows me to add a noSearch parameter to a page and skip it
- `{{- if gt $i 0 }},{{ end -}}` add commas between the jsons

- Add a field for date, url, title, summary, content, tags, and level
```
{
    "date":"{{ .Date.Unix }}", 
    "url":"{{ .Permalink }}", 
    "title":{{ .Title | jsonify  }}, 
    "summary":{{ with .Description}}{{ . | plainify | jsonify }}{{ else }}{{ .Summary | plainify | jsonify }}{{ end }}, 
    "content":{{ .Content | plainify | jsonify }},
    "tags":[ {{- $t := 0 }}{{- range .Param "tags" -}}{{ if gt $t 0 }},{{ end }}{{ . | jsonify }}{{ $t = add $t 1 }}{{ end -}} ], 
    "level":[ {{- $t := 0 }}{{- range .Param "difficulties" -}}{{ if gt $t 0 }},{{ end }}{{ . | jsonify }}{{ $t = add $t 1 }}{{ end -}} ] 
}
```
And that is how you do this.
I even added it to a recipes website so I could do some magic on recipes without having to parse and clean the html.
