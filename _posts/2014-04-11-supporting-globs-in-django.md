---
layout: post
title: Supporting Globs in Django
date: "2014-04-11T02:45:00+05:00"
tags: 
  - python
  - django
tumblr_url: "http://alixedi.tumblr.com/post/82309996867/supporting-globs-in-django"
published: true
---

Glob is a syntax for specifying search queries that support wildcard characters. Glob is simpler than regular expressions and therefore is relatively easier to learn and use. Glob is particularly popular in Unix-like environments for instance specifying a pattern for files to delete in the terminal: 

> rm *.txt

Django does not have drop-in support for glob lookups in search and filter forms etc. In comes [GlobField](https://gist.github.com/alixedi/7939804).