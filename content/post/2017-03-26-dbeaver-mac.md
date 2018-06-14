---
title: "Installing DBeaver on a Mac"
date: 2017-03-26T21:35:50-08:00
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "DBeaver", ]
aliases:
  - "/2017-03-26-DBeaver-on-Mac.html"
---

# 0) What is [DBeaver](http://dbeaver.jkiss.org/)?

Quite simply DBeaver is the best multi-database SQL IDE that I've used. It supports every JDBC connection that I've thrown at it and has advanced features for some of the more popular databases such as Mysql & Postgres. Many thanks to [serge-rider](https://github.com/serge-rider) for creating such an awesome tool.

# 1) Install Java

First we need to install java which can be easily by running the following command in terminal ([homebrew required](https://brew.sh/)):

```bash
brew cask install java
```

Note: Previous versions of this article instructed an installation of the cask `jce-unlimited-strength-policy` but that has been removed as its contents have been incorporated into the cask `java` with the release of 9.0

## Notes

  * I recommend the newest version of Java as DBeaver regularly depreciates old versions of Java
    * [Java SE6](https://support.apple.com/kb/DL1572?locale=en_US) is not supported

# 2) Install DBeaver

  1. Download the [latest version](http://dbeaver.jkiss.org/download/) | [Github Alternate](https://github.com/serge-rider/dbeaver/releases)
  1. After downloading drag and drop into your application folder
    * The first time you run the application you may need to right-click on the application and then press open

Congratulations you've installed DBeaver!

Your next step is configuring a connection(s) to your database(s).
