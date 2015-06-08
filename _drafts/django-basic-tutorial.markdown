---
layout: post
title: "Django Basic Tutorial"
categories: python django
---

[Tutorial Link](https://docs.djangoproject.com/en/1.8/intro/tutorial01/)

## Install

{% highlight Bash %}
$ pip install django #install the official release
{% endhighlight %}

### Verify

{% highlight python %}
import django
print(django.get_version())
{% endhighlight %}

## Creating a project

{% highlight Bash %}
$ django-admin startproject mysite
{% endhighlight %}

We are supposed to put the **code** in some directory **outside** of the document root, such as **/home/mycode**

{% highlight Bash %}
mysite/
    manage.py #command line utility
    mysite/ #package (e.g. mysite.urls)
        __init__.py 
        settings.py
        urls.py
        wsgi.py
{% endhighlight %}

## Database setup

If by default we use **sqlite3** we don't have to touch anything.

{% highlight Bash %}
$ python manage.py migrate
{% endhighlight %}

## Development server

 You don’t need to restart the server for code changes to take effect. 

{% highlight Bash %}
$ python manage.py runserver
#or
$ python manage.py runserver 8080 #to run it in another port
{% endhighlight %}

## Project vs apps

A project is a collection of configuration and apps for a particular Web site. A project can contain multiple apps. An app can be in multiple projects.

## Creating an App

{% highlight Bash %}
$ python manage.py startap polls
{% endhighlight %}

{% highlight Bash %}
polls/
    __init__.py
    admin.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
{% endhighlight %}

