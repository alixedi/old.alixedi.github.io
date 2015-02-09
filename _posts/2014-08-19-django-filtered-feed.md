---
layout: post
title: "Feeds sans noise - Custom RSS feeds for django"
date: "2014-08-19T23:51:27+05:00"
tags: 
  - html
  - python
  - django
  - RSS
  - feed
  - syndication
  - email
published: true
---

So the average-joe RSS is binary ie either you subscribe to a feed or you don’t. This approach results in a ridiculous amount of junk in our inbox. What if we could `define` the feed that we would like to subscribe to? Thanks to the stellar [django syndication framework](https://docs.djangoproject.com/en/dev/ref/contrib/syndication/) and [django filters](https://github.com/alex/django-filter), I was able to hack together a fix.

If you have a `Book` model like so:

    {% highlight python  %}
    class Book(models.Model):
        name = models.CharField(max_length=256)
        pages = models.IntegerField()

    def __unicode__(self):
        return self.name
    {% endhighlight  %}

A [django filters](https://github.com/alex/django-filter) `FilterSet` like so:

    {% highlight python  %}
    class BookFilterSet(django_filters.FilterSet):
        pages = NumberFilter(lookup_type='lt')
        class Meta:
            model = Book
            fields = ['pages']
    {% endhighlight  %}

A `FilteredFeed` class like so:

    {% highlight python  %}
    class BookFilteredFeed(BaseFilteredFeed):
        model = Book
        filter_set = BookFilterSet
        title = "BookFeed"
        link = "http://localhost:8000"
        description = "Alerts for new books!"

        def item_link(self, item):
            return reverse('book_detail', 
                           args=[item.id])
    {% endhighlight  %}

Hook up the necessary urls like so:

    {% highlight python  %}
    urlpatterns = patterns('',
        url(r'^books/feed$', 
            BookFilteredFeed.as_view(), 
            name='book_feed'),
    )
    {% endhighlight  %}

And finally, if we have the following 3 books in our DB:

1.  Introduction to Python (100 pages)
2.  Introduction to C (300 pages)
3.  Javascript - The good parts (300 pages)

Hitting [http://localhost:8000/books/feed](http://localhost:8000/books/feed) will give you an RSS feed includes:

-   Introduction to Python
-   Introduction to C
-   Javascript - The good parts

And hitting [http://localhost:8000/books/feed?pages=200](http://localhost:8000/books/feed?pages=200) will give you an RSS feed that just includes:

-   Introduction to Python

You users will forever remain grateful for sparing them the deluge that follows a binary subscription. You will be hailed the king of syndication, worshipped as a rock star and live happily ever after. The best part is that it takes a minute to get started:

> pip install django_filtered_feed

Followed ofcourse by including `filtered_feed` in your `INSTALLED_APPS`.

    {% highlight python  %}
    INSTALLED_APPS = (
        ...
        'filtered_feed',
        ...
    )
    {% endhighlight  %}
