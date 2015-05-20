---
title: Grammar and Objects
layout:post
---

## Gramar

* Whitespace
* Names
* Numbers
* Strings
* Statements
	* Falsy values
	false
	null
	undefined
	empty string ''
	number 0
	number NaN

	* switch
	* case
	* while
	* for
	* do
	* try
	* throw
	* return
	* break
	* expression
		*precedence
			* . [] ()
			* delete new typeof + - !
			* / %
			* + -
			* >= <= > <
			* === !==
			* &&
			* ||
			* ?:

## Objects

The simple types of Javascript are
* numbers
* strings
* booleans
* null
* undefined

All the other values are **objects**!

Javascript includes a prototype linkage feature that allows one object to inherit the properties of another.

## Object Literals

{% highlight javascript %}
var empty_object = {};

var stooge = {
	"first-name": "Jerome",
	"last-name": "Howard"
};

var flight = {
	airline: "Oceanic",
	number: 815,
	departure: {
		IATA: "SYD",
		time: "2004-09-22 14:55",
		city: "Sydney"
	},
	arrival: {
		IATA: "LAX",
		time: "2004-09-23 10:42",
		city: "Los Angeles"
	}
};
{% endhiglight %}

## Retrieval
{% highlight javascript %}
//Both ways are correct but the second one is preferred
var var1 = stooge['first-name'];
var var2 = flight.deaprture.IATA;
{% endhighlight %}

### Default Values
{% highlight javascript %}
var status = flight.status || "unknown";
{% endhighlight %}

Attempting to retrieve values from *undefined* will trhow a **TypeError** exception.

## Reference

Objects are passed around by **reference**. They are **never copied**.

## Prototype

Every object is linked to a prototype object from which it can inherit properties. All
objects created from object literals are linked to **Object.prototype**, an object that
comes standard with JavaScript.

### Delegation
**The prototype link is used only in retrieval**. If we try to retrieve a property value from
an object, and if the object lacks the property name, then JavaScript attempts to
retrieve the property value from the prototype object. This is called delegation.

## Reflection

Usually it's very helpfu to use **typeof**. But scare must be taken because any property on the **prototype chain** can produce a value.

### hasOwnProperty

It returns true if the object has a particular property. The *hasOwnProperty* does not look at the prototype chain.

{% highlight javascript %}
myObject.hasOwnProperty('propertyName');
{% endhighlight %}

## Enumeration

The for in statement can loop over all of the property names in an object. The enumeration will include all of the properties **including functions and prototype properties**. If you want to filter out these values you have to use the **hasOwnProperty**.

{% highlight javascript %}
var propertyName;
for(propertyName in myObject){
	if(typeof myObject[propertyName] !== 'function' && myObject.hasOwnProperty(propertyName)){
		document.writeln(name + ': ' + myObject[propertyName]);	
	}
	
}
{% endhighlight %}

If we want a specific order whe need an **array**.
{% highlight javascript %}
var i;
var properties = [
	'first-name',
	'middle-name',
	'last-name',
	'profession'
];
for(i = 0; i < properties.length; i +=1 ){
	document.writeln(properties[i] + ': ' myObject[properties[i]]);
}
{% endhighlight %}

## Delete

The delete operator can be used to remove a property from an object.

Removing a property from an object may allow a property from the prototype linkage to shine through.

{% highlight javascript %}
delete myObject.propertyOne;
{% endhighlight %}

## Global Abatement

One way to minimize the use of global bariables is to create a single global variable for your application:

{% highlight javascript %}
var MYAPP = {};
{% endhighlight %}

