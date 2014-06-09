---
layout: post
title: Introducing Shootstrap
date: "2014-04-24T19:35:00+05:00"
tags: 
  - bootstrap
  - Css
  - HTML
tumblr_url: "http://alixedi.tumblr.com/post/83709819624/introducing-shootstrap"
published: true
---

Lets you apply bootstrap css on selected divs like a boss:

{% highlight html %}
<div class="shoot">
  <div class="jumbotron">
    <h1>Look at me I have Bootstrap baby!</h1>
  </div>
</div>
{% endhighlight %}

{% highlight html %}
<div class="dont_shoot">
  <div class="jumbotron">
    <h1>Show Off</h1>
  </div>
</div>
{% endhighlight %}

Often, this is a life saver. For instance in case of the excellent Google Chart Editor that gets totally messed up on any page with bootstrap in it.

In order to user Shootstrap, simply replace your regular bootstrap.css with shootstrap.css. You can compile shootstrap.css from the source using LESS etc or just use the pre-compiled one I have put here.

This project is a fork of Twitter’s Bootstrap.

Have fun.