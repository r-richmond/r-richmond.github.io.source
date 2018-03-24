---
title: "First Blog With Pelican"
date: 2017-03-03
draft: false
categories : [
    "Tinkerer",
]
tags: ["Blogging",
      "Python",
      ]
aliases:
  - "/2017-03-03-Pelican-Intro.html"
---

## Update 2018-03-18: I've since moved to Hugo

This is my first blog post using Pelican and Markdown. A lot of the content below is to be used as reference mostly for myself and any others who are exploring using Python3, Pelican, & Markdown to create a blog.

How to get up and running

```bash
mkvirtualenv personal_blog
pip install pelican
pip install markdown
pip install fabric3
pip install ghp-import
pip install webassets
npm install less -g
cd Dropbox/projects/python/personal_blog/
git clone https://github.com/r-richmond/rirchmond.github.io.git
git submodule add https://github.com/textbook/bulrush.git
git submodule add https://github.com/getpelican/pelican-plugins.git
```

Running commands using Fab3 which help prepare posts
```bash
fab rebuild
fab preview
fab serve
fab clean
fab gh_pages
fab reserve
```

This [post](http://nafiulis.me/making-a-static-blog-with-pelican.html) was very helpful as well

I followed this [post](http://www.curtismlarson.com/blog/2015/04/12/github-pages-google-domains/) to setup my custom domain
