---
layout: post
title: "Javascript Arrays"
---

Arrays in javascript are significantly slower than a real array.

## Array Literals

{% highlight javascript %}
var empty = [];

var numbers = [
        'zero','one','two','three'
];
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
{% endhighlight %}

## Delete

{% highlight javascript %}
//delete 1 element from position 2
var numbers = [1,2,3,4];
numbers.splice(2,1); // 1,2,4
{% endhighlight %}

## Enumeration

{% highlight javascript %}
var i;
for (i = 0; i < myArray.length; i += 1) {
        document.writeln(myArray[i]);
}
{% endhighlight %}