---
layout: post
title: "Rails, Working with a database"
categories: ruby rails databse
---

##Active Record: ORM (Object-Relational Mapping) on Rails

{% highlight ruby %}
class Book < ActiveRecord::<Base
end
{% endhilghlight %}

Active Record is database agnostic, so it doesn't care which database software you use, and it supports nearly every database out there.

**You can also use another ORM like *DataMapper* **

### Conventions

* Class names are singular; table names are plural
* Tables contain an identity column named identity

e.g.
events --> Event
people --> Person
categories -> Category
order_items ->OrderItem

## Rails Console

$ Article.column_names
$ Article.methods.size
