---
layout: post
title: Introducing Django Coffee Table
date: "2014-05-29T18:05:00+05:00"
tags: 
  - python
  - django
  - table
  - HTML
tumblr_url: "http://alixedi.tumblr.com/post/87189084896/introducing-django-coffee-table"
published: true
---

I was reading Things a little bird told me by Twitter co-founder Biz Stone the other day. I will review the work later but what stuck out as the take-away message is:

> Constraints drive innovation.

Over at [Bitswits](www.bitswits.com) - the startup that I have been running for the past couple of years, the biggest problem is HR. We cannot for the life of us get decent Python let alone Django developers in Pakistan. It seems .NET has a death grip on the campuses.

On the other hand, it is significantly easier to hire good front-end people with some experience in templating. As a result, during the past year or so, Bitswits have evolved a spin on Django’s MVT (Model-View-Template) separation that we like to call M/V/T.

Essentially, a serious dearth of good Python hackers forces us to push every bit of presentation logic out to the templates. We do this by making template-composable web components.

Coffee Table is one such project. Now I am not a big fan of re-inventing the wheel. So I thoroughly fiddled away at all the alternatives. Unfortunately, following example represents the state of affairs:

{% highlight Python %}
class SimpleTable(Table):
	class Meta:
        model = Simple
        attrs = {'class': 'mytable'}
        sequence = ('name', 'surname')
{% endhighlight %}

Enough said. Now take a look at the equivalent Coffee Table syntax. Remember that we are not writing Python anymore. This takes place in Django templates:

{% highlight Python %}
{% raw %}
{% coffee_table 
	objects
	field_accessors='name, surname' 
	table_class='table table-condensed' 
%}
{% endraw %}
{% endhighlight %}

And this is just the start. Following example shows off the full set of options:

{% highlight Python %}
{% raw %}
{% coffee_table 
	objects 
	field_accessors='name, surname'
	table_class='table table-condensed'
	paginate_by=10
	checkbox_column=True
	primary_key_column=True
	help_text=True 
%}
{% endraw %}
{% endhighlight %}

The result: HTML table that can be composed by HTML people. Problem solved.

So you ask: Wonderful! now how the heck do I use this? Well, you can get Coffee Table via cheese shop:

> pip install django_coffee_table

Include coffee_table in your INSTALLED_APPS. Set up dependencies according to their respective docs:

* linaro-django-pagination
* django-resort
* django-tag-parser

Now load up the template tags and rock-on like so:

{% highlight Python %}
{% raw %}
{% load coffee_table %}
{% coffe_table objects %}
{% endraw %}
{% endhighlight %}

If you find any issues, bones to pick, pat on the back or any other such business, head right over to [Github](https://github.com/alixedi) and shout.