---
layout: post
title: "Javascript Functions"
---

Functions are the fundamental modular unit of Javascript.

They are used for:

* Code reuse
* Information hiding
* Composition
* Behavior of objects

## Function Objects

Functions in javascript are objects.

Functions objects are linked to *Function.prototype* which itself linked to *Object.prototype*.

Every function is also created with two additional hidden properties: 
* the function's context
* the code that implements the function's behavior

The thing that is special about functions is that they can be invoked.

## Function Literal

{% highlight javascript %}
function optionalNameOfTheFunction(param1, param2){
 //statements 
}
{% endhighlight %}

An inner function also enjoys access to the parameters and variables of the functions it is nested within. The function object created by a function literal contains a link to that outer context. This is called *closure*.

## Invocation

Every function receives two additional parameters: **this** and **arguments**.

The **this** parameter is very important in object oriented programming, and its value is determined by the *invocation pattern*.

There are four patterns of invocation in Javascript. The patterns differ in how the bonus parameter **this** is initialized:

* method invocation pattern
* function invocation pattern
* constructor invocation pattern
* apply invocation pattern

### The Method Invocation Pattern

When a function is stored as a property of an object, we call it *method*.

{% highlight javascript %}
var myObject = {
        value:0,
        increment: function(inc){
                this.value += typeof inc === 'number' ? inc : 1;
        }
};
 myObject.increment(); //1
 myObject.increment(3); //4
{% endhighlight %}

The binding of this to the object happens at invocation time.

Methods that get their object context from this are called *pubic methods*.

### The Function Invocation Pattern

{% highlight javascript %}
function add(param1, param2){
        return param1 + param2;
}

var sum = add(3,6); //9
{% endhighlight %}

When a function is invoked with this pattern, **this** is bound to the global object.

A consequence of this error is that a method cannot employ an inner function to help it do its work because the inner function does not share the method's acceses to the object as it its **this** is bound to the wrong value.

By convention, we use **that**

{% highlight javascript %}
var myObject = {
        value:2,
        getValue : function (){
                return this.value;
        }
};
//augment myObject
myObject.double = function (){
        var that = this;

        var helper = function (){
                that.value = that.value + that.value;
        }

        helper();
};
myObject.double();
console.log(myObject.getValue()); //4
{% endhighlight %}

### The Constructor Invocation Pattern

Objects can inherit properties directly from other objects. The language is **class-free**.

If a function is invoked with the **new** prefix, then a new object will be created with a hidden link to the value of the function's *prototype* member, and *this* will be bound to that new object.

{% highlight javascript %}
var Quo = function (string){
        this.status = string;
}

Quo.prototype.getStatus = function (){
        return this.status;
};

var myQuo = new Quo("confused");
var myOtherQuo = new Quo("more confused");

console.log(myQuo.getStatus());
console.log(myOtherQuo.getStatus());
{% endhighlight %}

Functions that are intended to be used with the **new** prefix are called **constructors**. By convention, they are kept in variables with **capitalized** name.

### The Apply Invocation Pattern

Javascript is a **functional** object-oriented language, functions can have methods.

#### The Apply Method

It lets us construct an array of arguments to sue to invoke a function. It also lets us choose the value of *this*.

The first parameter is the value of *this* the second are the arguments.

{% highlight javascript %}
function add (param1,param2){
        return param1 + param2;
}

var array = [3,4];
var sum = add.apply(null,array); //sum is 7

{% endhighlight %}

{% highlight javascript %}
var Quo = function (string){
        this.status = string;
}

Quo.prototype.getStatus = function (){
        return this.status;
};

var statusObject = {
        status : 'OK'
};

var status = Quo.prototype.getStatus.apply(statusObject); // 'OK'


{% endhighlight %}

## Arguments

A bonus parameter that is available to functions when they are invoked is the *arguments* array (in fact it is an array-like object, it lacks all of the array  methods but length).
{% highlight javascript %}

var sum = function (){
        var i, sum 0;
        for(i=0; i < arguments.length; i += 1){
                sum += arguments[i];
        }
        return sum;
};

console.log(sum(4,8,15,16,23,42)); //108
{% endhighlight %}

## Return

A function always returns a value. If the *return* value is not specified, the *undefined* is returned.

If the function was invoked with the new prefix and the return value is not an object,
then this (the new object) is returned instead.

## Exceptions

{% highlight javascript %}
var add = function (a, b) {
        if (typeof a !== 'number' || typeof b !== 'number') {
                throw {
                        name: 'TypeError',
                        message: 'add needs numbers'
                };
        }
        return a + b;
}

var try_it = function ( ) {
        try {
                add("seven");
        } catch (e) {
                document.writeln(e.name + ': ' + e.message);
        }
}

try_it( );

{% endhighlight %}

## Augmenting Types

JavaScript allows the basic types of the language to be augmented. This also works for functions, arrays, strings, numbers, regular expressions, and booleans.

By augmenting the basic types, we can make significant improvements to the expressiveness of the language. Because of the dynamic nature of JavaScript's prototypal inheritance, all values are immediately endowed with the new methods, even values that were created before the methods were created.

One defensive technique is to add a method only if the method is known to be missing:
{% highlight javascript %}
        // Add a method conditionally.
        Function.prototype.method = function (name, func) {
                if (!this.prototype[name]) {
                        this.prototype[name] = func;
                }
        };
{% endhighlight %}

## Recursion

A *recursive* function is a function that calls itself, either directly or indirectly.

## Scope

## Closure

{% highlight javascript %}
var myObject = function (){
        var value = 0;

        return {
                increment: function (inc){
                        value += typeof inc === 'number' ? inc: 1;
                },
                getValue: function (){
                        return value;
                }
        };
}();
{% endhighlight %}

We are not assigining a function to *myObject*. We are assigning the result of invoking that function.

{% highlight javascript %}
var fade = function (node){
        var level = 1;
        var step = function (){
                var hex = level.toString(16);
                node.style.backgroundColor = '#FFF' +hex +hex;
                if(level < 15){
                        level += 1;
                        setTimeout(step,100);
                }
        };
        setTimeout(step,100);
}
{% endhighlight %}

## Callbacks

We pass a function parameter to the send_request_asynchronously function that will be called when the response is available.

## Module

We can use functions and closure to make modules.

**A module is a function or object that presents an interface but that hides its state and implementation**.

## Cascade

It is typical for methods that set or change the state of an object to return nothing. If we have those methods return this instead of undefined, we can enable cascades.

## Curry

Currying allows us to produce a new function by combining a function and an argument.

## Memoization

Functions can use objects to remember the results of previous operations, making it possible to avoid unnecessary work.
