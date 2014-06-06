---
layout: post
title: Introducing Django Sieve
date: '2014-06-05T15:53:00+05:00'
tags:
- django
- python
tumblr_url: http://alixedi.tumblr.com/post/87877410736/introducing-django-sieve
---
So we were developing a CRM-like system over at Bitswits. The users of the system were sales representatives of a telco. Without getting bogged down by the details, we were required to do the following from an access control perspective:

1. Each sales rep will be assigned a set of companies.

2. Each sales rep will be assigned a single country.

3. The sales rep will be able to access data from his assigned set of companies and the country *only*.


These cute little features morphed into a monster because of the following scenario:

So lets do a little operator overloading - if “>” signifies a foreign-key relation from the left-side operand to the right-side operand, we were dealing with situations such as:

    Rate > Tariff > Vendor > Company


Also, some of the relations were ManyToMany - if “»” signifies a ManyToMany relation from the left-side operand to the right-side operand:

    Rate > Tariff >> Client(s) > Comapny


Finally, consider the fact that the system had 100-odd views and we had a show-stopper. There was no way I could allow my precious Python devs to spend a couple of weeks writing and tuning queries by hand for what seemes like at least a couple of weeks.

Enter Sieve. Following is whole code that solved the problem.

Create the control model - the one that stores which sales rep has access to which companies and country:

class Sieve(models.Model):
    group = models.ForeignKey(''auth.Group'')
    companies = models.ManyToManyField(''Company'')
    country = models.ForeignKey(Country)

Identify the sieve model in your settings.py:

SIEVE_MODEL = ''crm.Sieve''

Over-ride the ModelManagers for the models that you want filtered:

class Country(models.Model):
        name = models.CharField(max_length=30)
        dialcode = models.DialcodeField()
        objects = SieveManager()

Rock-on like so:

class CoutryView(ListView):
    objects = Country.objects.sieve(user=request.user)

That is all. Site-wide filtering of user data based on predefined criteria without having to write queries for all the views.
