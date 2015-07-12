---
layout: post
title: "Angular Tests"
date: 2015-06-11 19:15:02
categories: javascript angularjs
---

## Fundamentals of TDD

* Knowing before you code
* Confidence in refactoring
* Documentation

## The Steps to make a *suit*

1. Test first
2. Making the cuts
3. Refactoring
4. Repeating previous steps

## Terms

* Function under test
* The 3 A's
        * Arrange
        * Act
        * Assert

## Testing doubles

A test *double* is an object that acts and is used in place of another object.

A Jasmine test double offers features like these:

* The count of calls on a function
* Stub a return value
* Pass a call to the underlying function

{% highlight javascript %}
jasmine.spyOn(objectUnderTest,'someFunction')
.and
.returnValue('stubbed value');

objectUnderTest.someFunction('param1','param2');
objectUnderTest.someFunction('param1','param2');

var callArgs = objectUnderTest.someFunction.call.argsFor(0);

console.log(callArgs); //['param1','param2']
console.log(objectUnderTest.someFunction.count); //2
console.log(objectUnderTest.someFunction()); //'stubbed value'
{% endhighlight %}

## Builder pattern

> Imagine an object with ten properties. How will test data be created for every property? Will the object have to be recreated in every test?

We create a **single** consistent object.

{% highlight javascript %}
var carBuilder = function (){
        var _resultCar = {
        	id: 1,
        	owner_ 'John Smith',
        	dateTime: new DateTime()      
        };

        this.build = function(){
        	return _resultCar;
        }

        this.setOwner = function (owner){
        	_resultCar.owner = owner;
        	return this;
        }

        this.setDateTime = function (datetime){
        	this.dateTime = datetime;
        	return this;
        }
};

var myCar = carBuilder.setOwner('James')
.setDateTime(new Date())
.build();
{% endhighlight %}

## Javascript testing frameworks

* Jasmine
* Selenium
* Mocha

## Testing with Karma

* describe
* it
* expect
* toBeTruthy

{% highlight javascript %}
describe('when testing karma', function (){
        it('should report a successful test', function (){
                expect(true).toBeTruthy();
        });
});
{% endhighlight %}

### Angular mocks

> The ngMock module provides support to inject and mock Angular services into unit tests. In addition, ngMock also extends various core ng services such that they can be inspected and controlled in a synchronous manner within test code.

{% highlight Bash %}
$ bower install angular-mocks
{% endhighlight %}

