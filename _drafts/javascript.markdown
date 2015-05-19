---
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
