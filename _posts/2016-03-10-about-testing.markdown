---
layout: post
sidebar-align: left
title: "About Testing"
categories: Testing
date:  2016-03-10 08:18:22
author: Pere Pages
---

* TOC
{:toc}

## Intro

+ Learn to read the code 
+ Mind your dependencies
+ Sharpen your Environment Ax

**There are no secrets with tests, but there are writing testable code! Properly managed dependencies!!**

## Why Test?

Because writing the test is easier then running the application.

**Testing is not like frosting**
The only way to make sure your test code is testable is to write the tests from the very beginning.

## Excuses

The only right one is: **"I DON'T KNOW HOW"**.

We have problems admitting we have problems writing tests. Of course it's going to be hard to write tests.

It's skill like any other skill, it needs practice. How to struture the code to make it testable.

## Write Tests First

+ Software Engineers
+ QA
+ Test Engineers

*The cake has alreaby been baked*. That's the main reason why tests do not work.

**How would you write HARD TO TEST code?**
Global State code! Because it is hard to control.

The tests have to be EASY to read. 

The difficulty of **the TEST it's about the STRUCTURE of the code. Not what the CODE does**.

**Some of the worst case scenarios**
+ Global State aka Singleton
+ Law of Demeter Violation
+ Global reference to time
+ Hard-coded new Operator
+ Lack of Dependency Injection

### Real Issues

+ Mixing new with logic
+ Looking for things
+ Work in constructor
+ Global state
+ Singletons
+ Static methods
+ Deep inheritance
+ Too many conditionals
+ Mixing Service/Value
+ Mixing Concerns

**Dependency Injection!!**
What are the fundamentals items you need to make your job done.

## Testable Code

+ Good OO
+ Dependency Injection
+ Test Driven Development
+ A whole lot about un-testable code

**There is no secret to writing tests... there are only secrets to writing testable code!**

## Tests

+ Scenario Tests
+ Functional Tests
+ **Unit Tests**

70 : 20 : 10

Tests should be run on every save.


## Unit Testing a Class

Control the dependencies. I am not going to look beyond the class I am testing.

No Global Objects, only objects being past in.

**Friendly (the dependency) does not have to be a mock**. You can perfectly create a situation for a test with a Class.

## Write a test

You have to know why they are written. **Can you run an implementation, given the test?!**

**Executable Specs!!!**
Specs are test with syntatctic sugar (... and sugar makes everything taste better).

+ Assume the code is yet to be written
+ Demonstrate a single behavior per spec
+ Tell a story

Remove form your class dependencies with Filesystem or Database. Onply pass dependencies. Use Factories.

We can consider two kind of objects that we deal with:

+ Value Objects
+ Service Objects

Services are *beasts* that talk to another objects and should be mocked.

### Unit Testing Review

* new operators are dangerous
* Ask for what you need
    - If you need it, then you must interact with it
    - Law of Demeter
* Global State is testibility nightmare
* Doing work in construtor is dangerous

**Example**
You are essentially defining the API. You are doing the API first, implementation later.

Class InboxSyncerSpec{
    
    @Test itShouldSyncMessagesFromPopSinceLastSync(){}

    @Test itShouldCloseConnectionEvenWhenExceptionThrown(){}

    //...
}

## Environment

It must be easier to write a test, and see the results run, then to write the code an run the actual application.

doing the right thing **<** doing the wrong thing

+ Set up your IDE to make running tests
+ Make sure your tets are fast
+ Spend time making your environment testable
    * This may be expensive at first, but will pay dividends
+ There are no easy fixes

Setting up a proper environment for your code is as important as writing testable code.

If the environment is not friendly no one will write or run any tests.

## Glossary

Perforce
CL = Changeless