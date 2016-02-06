---
layout: post
title:  "Dependency Injection With AngularJS"
date:   2015-10-12 17:00:23
categories: javascript programming angularjs
---

In general, there are only three ways an object can get a hold of its dependencies:

1. We can create it internally to the dependent.
2. We can look it up or refer to it as a global variable.
3. **We can pass it where it's needed.**

With dependeny injection, we're tackling the third way.

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Why

+ Removal of hard-coded dependencies. Thus making it possible to remove or change them at run time.
+ Ideal for testing. We can replace real objects in production environments with mocked ones.

## How

The pattern injects depended-upon resources into the destination when needed by automatically looking up the dependency in advance and providing the destination for the dependency.

As we write components dependent upon other objects or libraries, **we will describe its dependencies**. At run time, an **injector** will create instances of the dependencies and pass them along the **dependent consumer**.

## Example

```javascript
//Constructor
function SomeClass(greeter){
    this.greeter = greeter;
}
SomeClass.prototype.greetName = function (name){
    this.greeter.greet(name);
}
```

In order to get that **greeter** instance into **SomeClass**, the creator of **SomeClass** is responsible for passing in the **SomeClass** dependencies when it's created.

## $injector

Angular uses the **$injector** for managing lookups and instantiation of dependencies. The $injector is responsible for handling all instantiations of our Angular components, including our app modules, directives, controllers, etc.

When any of our modules boot up at run time, the **injector** is responsible for actually instantiating 

```javascript
angular.module('myApp', [])
    .factory('greeter', function (){
        return {
            greet: function(msg) {alert(msg);}
    }
    })
    .controller('MyController',
    function($scope, greeter){
        $scope.sayHello = function(){
            greeter.greet("Hello!");
    };
    });
```

```javascript
<div ng-app="myApp">
    <div ng-controller="MyController">
        <button ng-click="sayHello()">Hello</button>
    </div>
</div>
```

Behind the scenes.

Nowhere in the below example did we describe how to find the greeter; it simply *works*, as the injector takes care of finding and loaing it for us.

```javascript
//Load the app with the injector
var injector = angular.injector(['ng','myApp']);

// Load the $controller service with the injector
var $controller = injector.get('$controller');
var scope = injector.get('$rootScope').$new();

//Load the controller, ppassing in a scope which is how angular does it at runtime
var MyController = $controller('MyController',{$scope: scope});
```

## How the $injector works

AngularJS ueses an **annotate** function to pull properties off of the passed-in array during instantiation.

```javascript
injector.annotate(function($q,greeter) {});
```

## Annotation

1. by Inference
2. Explicit
3. Inline

### by Inference

Angular assumes that the function parameter names are the names of the dependencies, if not otherwise specified. Thus, it will call *toString()* on the function, parse and extract the function arguments, and then use the **$injector** to *inject* these arguments into the instantiation of the object.

> Note that this process will *only* worki with non-minified, non-obfuscated code, as Angular needs to parse the arguments intact.

### Explicit

With this annotation style, order is important, as the *$inject* aray must match the ordering of the arguments to inject. This method of injection *does* work with minification, because the annotation information will be packaged with the function.

### Inline Annotation

It allows us to pass an array of arguments instead of a function when defining an Angular object. The elements inside this aray are the list of injectable dependencies as trings, the last argument being the function definition of the object.

```javascript
angular.module('myApp')
    .controller('MyController',['$scope','greeter',function ($scope,greeter){
    //...
    }]);
```

## $inject API

It's relativle **rare** that we'll need to work directly with the **$injector**.

+ annotate()
+ get()
+ has()
+ instantiate()
+ invoke()

## ngMin

The **ngMin** tool allows us to alleviate the responsibility to define our dependencies explicitly. ngMin is a *pre-minifier* for Angular apps. It walks through Angular apps and sets up dependency injection for us.