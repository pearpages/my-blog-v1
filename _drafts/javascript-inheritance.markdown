---
layout: post
title: "Javascript Inheritance"
---

Javascript, being a loosely typed language, never casts.

What matters about an object is what it can do, not what it is descended from.

It is usually best to keep it simple.

## Pseudoclassical

The pseudoclassical form can provide comfort to programmers who are unfamiliar with JavaScript, but it also hides the true nature of the language.

## Object Specifiers

We can write a constructor that accepts a single object specifier.

{% highlight javascript %}
//instead of
var myObject = make(a,b,c,d);

//we can write
var myObject = make({option1: 'a', option2: 'b', option3: 'c', option4: 'd'});
{% endhighlight %}

## Prototypal

You start by making a useful objet. You can then make many more objects that are like that one.

{% highlight javascript %}
var myMammal = {
        name : 'Herb the Mammal',
        getName : function (){
                return this.name;
        },
        says: function (){
                return this.saying || '';
        }
};
{% endhighlight %}


## Functional 

## Parts

