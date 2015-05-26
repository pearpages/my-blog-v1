---
layout: post
title: "Javascript Arrays"
categories: javascript arrays
date:  2015-05-26 19:40:22
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

> An array is a linear allocation of memory in which elements are accessed by integers that are used to compute offsets.

JavaScript provides an object that has some array-like characteristics. Arrays in javascript are significantly slower than a real array. They inherit from *Array.prototype* and have a larger set of useful methods and the *length* property.

Javascript allows an array to contain a **mixture of values**.

## The Rule

> When the property names are small sequential integers, you should use an array. Otherwise, use an object.

## Array Literals

{% highlight javascript %}
var empty = [];

var numbers = [
        'zero','one','two','three'
];

empty[1]; //undefined
numbers[1]; //'one'

empty.length; //0
numbers.length; //10
{% endhighlight %}

## Length

{% highlight javascript %}
var myArray = [];
myArray.length; //0

myArray[1000000] = true;
myArray.length // 1000001

{% endhighlight %}

The length can be set explicitly. Making the length larger does not allocate more space for the array. Making the length smaller will cause all properties with a subscript that is greater than or equal to the new length to be deleted.
{% highlight javascript %}
var numbers = ['one','two']

numbers[numbers.length] = 'new'; // 'one','two','new'
//or
numbers.push('another'); //'one','two','new','another'
{% endhighlight %}

## Delete

{% highlight javascript %}
//delete 1 element from position 2
var numbers = [1,2,3,4];
numbers.splice(2,1); // 1,2,4

numbers.length = 2; //1,2
{% endhighlight %}

## Enumeration

{% highlight javascript %}
var i;
for (i = 0; i < myArray.length; i += 1) {
        document.writeln(myArray[i]);
}
{% endhighlight %}

## Checking if is Array

In the same window or frame.

{% highlight javascript %}
var is_array = function (value) {
        //we check if it's falsy because typeof null give us 'object'
        return value && 
        typeof value === 'object' &&
        value.constructor === Array;
};
{% endhighlight %}

In a different window or same.

{% highlight javascript %}
var is_array = function (value) {
        return value &&
        typeof value === 'object' &&
        typeof value.length === 'number' &&
        typeof value.splice === 'function' &&
        !(value.propertyIsEnumerable('length'));
};
{% endhighlight %}

## Methods

We can *augment* the type (**Array.method**) or add the methods directly to an individual array.

### array methods

* array.concat(item...)
* array.join(separator)
* array.pop()
* array.push(item...)
* array.reverse()
* array.shift()
* array.slice(start,end)
* array.sort(comparefn)
* array.splice(start,deleteCount,item...)
* array.unshift(item...)
