---
layout: post
title: "Javascript Inheritance"
categories: jasvascript inheritance
date: 2015-05-25 20:40:23
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

In the classical languages, inheritance provides two useful services. 

* First, it is a form of code reuse. If a new class is mostly similar to an existing
class, you only have to specify the differences.
* It includes the specification of a system of types.

Javascript, being a loosely typed language, never casts.

What matters about an object is what it can do, not what it is descended from.

It is usually best to keep it simple.

## Pseudoclassical

The pseudoclassical form can provide comfort to programmers who are unfamiliar with JavaScript, but it also hides the true nature of the language.

When a function object is created, the Function constructor that produces the function object runs some code like this:
```javascript
this.prototype = {constructor: this};
```

```javascript
var Mammal = function (name) {
	this.name = name;
};
Mammal.prototype.getName = function ( ) {
	return this.name;
};
Mammal.prototype.says = function ( ) {
	return this.saying || '';
};
```

### Inheritance

We can make another *pseudoclas* that inhertis from Mammal by defining its constructor function and replacing its *prototype* with an instance of Mammal

```javascript
var Cat = function (name) {
	this.name = name;
	this.saying = 'meow';
};
// Replace Cat.prototype with a new instance of Mammal
Cat.prototype = new Mammal( );
```

## Object Specifiers

We can write a constructor that accepts a single object specifier. It's useful when we have a very large number of parameters.

```javascript
//instead of
var myObject = make(a,b,c,d);

//we can write
var myObject = make({option1: 'a', option2: 'b', option3: 'c', option4: 'd'});
```

## Prototypal

You start by making a useful objet. You can then make many more objects that are like that one.

### Differential inheritance

> By customizing a new object, we specify the differences from the object on which is based.

```javascript
var myMammal = {
        name : 'Herb the Mammal',
        getName : function (){
                return this.name;
        },
        says: function (){
                return this.saying || '';
        }
};

// We can then customize the new instances:
var myCat = Object.create(myMammal); //<-- !!!
myCat.name = 'Henrietta';
myCat.says = 'meow';
myCat.getName = function (){
	return this.says;
};
```

## Functional 

We create *privacy*  using the *module pattern*.

```javascript
//spec object contains all of the information that the constructor needs to make an instance. And they could be copied into private variables
var constructor = function (spec, my) {
var that, other_private_instance_variables;
my = my || {};

//Add shared variables and functions to my

//that = a new object; 

//Add privileged methods to that

return that;
};
```

Reminder. We can create objects:

* object literal
* call a constructor with *new*
* use the Object.create
* call a function that returns an object

See the example with Mammal

```javascript
var mammal = function (spec) {
	var that = {};
	that.get_name = function ( ) {
		return spec.name;
	};
	that.says = function ( ) {
		return spec.saying || '';
	};
	return that;
};
var myMammal = mammal({name: 'Herb'});

//see how Cat inhertis from Mammal

var cat = function (spec) {
	spec.saying = spec.saying || 'meow';
	var that = mammal(spec);
	that.get_name = function ( ) {
		return that.says( ) + ' ' + spec.name + ' ' + that.says( );
	return that;
};
var myCat = cat({name: 'Henrietta'});
```

### Durable Object

> If we create an object in the functional style, and if all of the methods of the object make no use of *this* or *that*, then the object is **durable**. A **durable** object is simply a collection of functions that act as capabilities.

### Superior Method

```javascript
Object.method('superior', function (name) {
	var that = this, method = that[name];
	return function ( ) {
		return method.apply(that, arguments);
	};
});
```

## Parts

We can compose objects out of sets of parts.