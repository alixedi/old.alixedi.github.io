---
layout: post
title: Introducing Django Sieve
date: "2014-06-05T15:53:00+05:00"
tags: 
  - django
  - python
published: true
---

So we were developing a CRM-like system over at [Bitswits](www.bitswits.com). The users of the system were sales reps of a telco. Without getting bogged down by the details, we were required to do the following from an access control perspective:

1. Each sales rep will be assigned a set of companies.

2. Each sales rep will be assigned a single country.

3. The sales rep will be able to access data from his assigned set of companies and the country *only*.

These cute little features morphed into a monster because of foreign-key and many-to-many relationshipd linking almost all the models (~50) in the system to comapny and country.

There was no way I could allow my precious Python devs to spend a couple of weeks writing and tuning queries by hand for 100s of views.

Enter Sieve. I spent a couple of days writing it. After which, following code solved the problem:

Create the control model - the one that stores which sales rep has access to which companies and country:

{% highlight Python %}
class Sieve(models.Model):
	group = models.ForeignKey('auth.Group')
	companies = models.ManyToManyField('Company')
	country = models.ForeignKey('Country')
{% endhighlight %}

Identify the sieve model in your settings.py:

{% highlight Python %}
SIEVE_MODEL = 'crm.Sieve'
{% endhighlight %}

Over-ride the ModelManagers for the models that you want filtered:

{% highlight Python %}
class Country(models.Model):
  	name = models.CharField(max_length=30)
	dialcode = models.DialcodeField()
	objects = SieveManager()
{% endhighlight %}

Rock-on like so:

{% highlight Python %}
class CoutryView(ListView):
	objects = Country.objects.sieve(user=request.user)
{% endhighlight %}

That is all. Site-wide filtering of user data based on predefined criteria without having to write queries for all the views.