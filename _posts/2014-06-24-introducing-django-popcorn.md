---
layout: post
title: Introducing Django Popcorn
date: "2014-06-24T01:29:00+05:00"
tags: 
  - python
  - django
published: true
---

Add-another pop-ups a la `django-admin`. 

The popup views are implemented using a mixin to the generic CreateView. Also, the popups now support permissions. As a result, a user will only get the `add-another` link next to a ForeignKey or a ManyToMany field if he has the add permission for the target model. In order to install, django-popcorn, use pip: :

    pip install django_popcorn

In order to use django-popcorn in your project, follow these steps: 

1. Include the following in your `INSTALLED_APPS` settings: :

    'popcorn',

2. Add this to your `settings.py` (If you do not already have it): :

    {% highlight python  %}
    TEMPLATE_CONTEXT_PROCESSORS = (
        "django.contrib.auth.context_processors.auth",
        "django.core.context_processors.debug",
        "django.core.context_processors.i18n",
        "django.core.context_processors.media",
        "django.core.context_processors.static",
        "django.contrib.messages.context_processors.messages",
        "django.core.context_processors.request",
        "popcorn.context_processors.admin_media_prefix",
    )
    
    POPCORN_MODELS = ('auth.Group', 'auth.Permission')
    {% endhighlight  %}

3. Add the following to your `base.html` template: :

    {% highlight  html %}
    <script src="{{ ADMIN_MEDIA_PREFIX }}js/admin/RelatedObjectLookups.js"></script>
    {% endhighlight  %}

4. We will create a view for `auth.User` and use the utility `get_popcorn_urls` function to generate popcorn views and urls: :

    {% highlight python %}
    urlpatterns = patterns('',
        url(r'^$', CreateView.as_view(model=User, success_url='.'), name='auth_user_create'),
        url(r'^admin/', include(admin.site.urls)),
    )

    urlpatterns += get_popcorn_urls()
    {% endhighlight %}

7. Render your forms like so: :: 

    {%  highlight html %}
    {% raw %}
    <form method="POST" action="{{ request.get_full_path }}">
        {% csrf_token %}
        {% include 'popcorn/form.html' %}
        <button type="submit">Submit</button>
        <a href="../">Cancel</a>
    </form>
    {% endraw  %}
    {% endhighlight  %}

Thats it! sync your DB, run the dev server and fire up your browser at localhost. You should see a form wthout the `add-another` links. This is because popcorn add-another links are only enabled for users who have add permission for the target model. Now log-in - possibly via admin after enabling it and hit localhost again. You should see a little `+` next to ForeignKey and ManyToMany fields. Click it and the add-another popup would appear. If you are having any problems, please check out the test project for a working implementation.
