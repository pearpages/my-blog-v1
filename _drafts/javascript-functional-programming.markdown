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

## Programming Techniques

## Category Theory

## Advanced topics and pitfalls

## Functional and Object-oriented programming




