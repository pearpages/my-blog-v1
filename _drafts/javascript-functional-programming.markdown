---
layout: post
title: "Javascript Funcitonal Programming"
categories: category1 category2
date:  2015-05-26 19:40:22
---

#### Contents
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Introduction

> While imperative code tells the machine, step-by-step, what it needs to do to solve the problem, functional programming instead seeks to describe the problem mathematically so that the machine can do the rest.

### What makes a language functional? 

**Functional programming cannot be performed in C. Functional programming cannot be performed in Java (without a lot of cumbersome workarounds for "almost" functional programming).**

| Characteristic | Imperative | Functional |
|:--|:--|:--|
| Programming Style | Perform step-by-step tasks and manage changes in state | Define what the problem is and what data transformations are needed to achieve the solution |
| State Changes | Important | Non-existent |
| Primary Flow Control | Loops, conditionals, and function calls | Function calls and recursion |
| Primary Manipulation Unit | Structures and class objects | Functions as first-class objects and data sets |

The syntax of the language must allow for certain design patterns, such as:

+ an inferred type system
+ anonymous functions
+ Lambda calculus
+ the interpreter's evaluation strategy should be non-strict and call-by-need*

* also known as deferred execution, which allows for immutable data structures and non-strict, lazy evaluation.

### Is Javascript a functional programming language?

> JavaScript is not a pure functional language. 

What's lacking is 

* lazy evaluation -> Lazy.js
* built-in immutable data -> programmer discipline
* it isn't also very good with recursion due to the way it handles tail calls -> *Tampolining*

### Advantages

* Cleaner code
* Modularity
* Reusability
* Reduced coupling
* Mathematically correct

The key to identifying functions that can be written in a more functional way is to look for **loops** and **temporary variables**, such as words and count instances in the preceding example. We can usually do away with both temporary variables and loops by replacing them with **higher-order functions**.

### Main Concepts

+ Self-invoking functions and closures: the function defined in the closure 'remembers' the environment in which it was created
+ Higher-order functions: take another function as an input or return a function as the output
+ Pure functions: return a value computed using only thei nputs passed to it
+ Anonymous functions: allow us the ability to define ad-hoc logic, on-the-spot and as needed. They are the embodiment of **Lambda calculus**
+ Method chains: multiple functions are applied to an object one after another
+ Recursion: a function that calls itself
+ Divide and conquer: recusively break problems into smaller instances
+ Lazy evaluation: non-strict evaluation, call-by-need and deferred execution, the result of a function it is not calculated until it is needed

### Javascript basic toolkit

* map()
* filter()
* reduce()

In javascript they only work in Arrays.

#### Callback

A callback() function is used for passing to other functions for them to use

#### Array

* forEach
* concat
* reverse (but it doesn't return a new Array!!)
* sort (the same as reverse)
* every, some

## Environment

> Underscore has become the standard functional javascript library in the eyes of many.

Underscore is actually a reimplementation of **Ruby's Enumerable module**, which explains why *CoffeeScript* was also influenced by Ruby.

+ map()
+ find()
+ invoke()
+ pluck()
+ sortyBy()
+ groupBy()

```javascript
var g = _.chain(greetings)
.sortBy(function(x) {return x.value.length})
.pluck('origin')
.map(function(x) {return x.chart(0).toUpperCase()+x.slice(1)})
.reduce(function(x,y) {return x + ' ' + y}, '')
.value();
```

### Functional libraries for JavaScript

+ Underscore.js
+ [Fantasy Land](https://github.com/fantasyland/fantasy-land)
+ Bilby.js
+ Lazy.js
+ Bacon.js
+ Functional
+ wu.js
+ sloth.js
+ stream.js
+ **Lo-Dash.js**
+ Sugar
+ from.js
+ JSLINQ
+ Boiler.js
+ Folktale
+ jQuery

## Implementig Functional Programming Techniques

### Partial function application

Partial application in JavaScript is the process of binding values to one or more arguments of a function that returns another function that accepts the remaining, unbound arguments. 

### Currying

Currying is the process of transforming a function with many arguments into a function with one argument that returns another function that takes more arguments as needed.

### Apply, call and the this keyword

In pure functional languages, functions are not invoked; they're applied.

#### Call()

```
fun.call(thisArg[, arg1[, arg2[, ...]]])
```

The call() function lets you define the *this* keyword as the first argument.

```javascript
// normal way
['Hello', 'world'].join(' ');
```

```javascript
// using call
Array.prototype.join.call(['Hello','world', ' ']);
```

It can be used, for example, to invoke anonymous functions:

```javascript
(function() {console.log(this.length)}).call([1,2,3]);
```

#### Apply()

The call() function accepts a list of arguments, the apply() function accepts an array of arguments.

```
fun.apply(thisArg, [argsArray])
```

#### Binding arguments

The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

```
fun.bind(thisArg[, arg1[, arg2[, ...]]])
```

```javascript
function Drum() {
    this.noise = 'boom';
    this.duration = 1000;
    this.goBoom = function() {console.log(this.noise)};
}

var drum = new Drum();
setInterval(drum.goBoom.bind(drum), drum.duration);
```

#### Function Factories

```javascript
function bindFristArg(func, a) {
    return function(b) {
        return func(a,b);
    }
}

var makePowersOf = bindFirstArg(bindFirstArg, Math.pow);
   var powersOfThree = makePowersOf(3);
   console.log(powersOfThree(2)); // 9
   console.log(powersOfThree(3)); // 27
```

#### Partial Application

Partial application is the process of binding values to one or more arguments of a function that returns a partially-applied function that accepts the remaining, unbound arguments.

The biggest flaw in this method is that the way in which the arguments are passed, as in how many and in what order, can be ambiguous. There's a better way to do this: currying.

##### From the left

```javascript
Function.prototype.partialApply = function() {
    var func = this;
    args = Array.prototype.slice.call(arguments);
    return function() {
        return func.apply(this, args.concat(
            Array.prototype.slice.call(arguments)
        ));
    }
}
```

##### From the right

```javascript
Function.prototype.partialApplyRight = function() {
    var func = this;
    args = Array.prototype.slice.call(arguments);
    return function() {
        return func.apply(
            this,
            [].slice.call(arguments,0)
            .concat(args));
    }
}
```

### Currying

Currying is the process of transforming a function with many arguments into a function with one argument that returns another function that takes more arguments as needed.

Currying allows much better control ofhow arguments are passed to the function.

> Currying does not work well with functions that accept variable numbers of arguments. For something like that, partial application is preferred.

```javascript
Function.prototype.curry = function (numArgs) {
    var func = this;
    numArgs = numArgs || func.length;

    // recursively acquire the arguments
    function subCurry(prev) {
        return function (arg) {
            var args = prev.concat(arg);
            if (args.length < numArgs) {
                // recursive case: we still need more args
                return subCurry(args);
            }
            else {
                // base case: apply the function
                return func.apply(this,args);
            }
        }
    }
    return subCurry([]);
}
```

### Function Composition

In functional programming, we want everything to be a function. We specially want unary functions if possible.

> **Unary** functions are functions that take only a single input. Functions with multiple inputs are **polyadic**, but we usually say *binary* for functions that accept two inputs and **ternary** for three inputs. Some functions don't accept specific number of inputs; we call those **variadic**.

#### Compose

Composing functions allows us to build complex funcitons from many simple, generic functions.

```javascript
Function.prototype.compose = function(prevFunc) {
    var nextFunc = this;
    return function() {
        return nextFunc.call(this,prevFunc,apply(this.arguments));
    }
}
```

Functions are applied from right to left.

#### Sequence - compose in reverse

```javascript
Function.prototype.sequence = function(prevFunc) {
    var nextFunc = this;
    return function() {
        return prevFunc.call(this,nextFunc.apply(this,arguments));
    }
}
```



## Category Theory

## Advanced topics and pitfalls

## Functional and Object-oriented programming
