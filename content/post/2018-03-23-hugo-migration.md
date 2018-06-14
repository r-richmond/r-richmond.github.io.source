---
title: "Moved to Hugo"
date: 2018-03-23
draft: false
categories : [
    "Tinkerer",
]
tags: ["Blogging",
      ]
---

## What was I using before

Previously I was using [Pelican](https://github.com/getpelican/pelican) a static site generator written in Python. Personally I'm a huge Python fan which led me to search out Pelican rather than go with a more popular solution such as [Jekyll](https://jekyllrb.com/).

## Why Change

As it turns out if you aren't going to be modifying the static site generator in anyway you don't need to concern yourself with the language that it is written in. This fact escaped me while I was seeking out Pelican. Coming to this realization opened up a world of possibilities and when I saw an article discussing Hugo and its killer feature, [Live Reload](https://gohugo.io/getting-started/usage/#livereload), I made the jump!

## Unique Migration tasks

The most complex task of this migration for me was ensuring that the old urls would point to the correct articles after I moved. fortunately Hugo made this dead simple via url [Aliases](https://gohugo.io/content-management/urls/#aliases).

Simply add the following to the front matter of the article you'd like migrate.
```
+++
aliases = [
    "/posts/my-original-url/",
    "/2010/01/01/even-earlier-url.html"
]
+++
```
