---
layout: post
title:  "AngularJs"
categories: angularjs web javascript
date:   2015-05-13 19:32:53
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Javascript client-side frameworks are sustainable models that offer many advantages over conventional web frameworks, such as simplicity, rapid development, speed of operation, testability, and the ability to package the entire application and deploy it to all movile devices and the Web with relative ease.

## MVC

AngularJS uses the MVC design pattern and embraces that pattern completely. The model, view, and controller are all clearly defined in AngularJS.

Business logic should almost always be placed in backend REST services whenver possible.

* Model: Stores the business data.
* View: Represents the model in UI.
* Controller: Responsible for coordinatin between model and view.

## RESTful web services

AngularJS's **resource** object lets developers interact with  REST services like standard objects.

AngularJS services help to greatly simplify an application by compartmentalizing client-side logic into single units of code.

## Dependency Injection

Dependency injection (DI) is a design pattern where dependencies are defined in an application as part of the configuration. Dependency injection helps you avouid having to manually create application dependencies.

One of its main advantages is that it reduces the need for boilerplate code, writing of which would normally be a time-consuming proccess.

DI also helps to mak an application more testable.

## Testing

There are two types of AngularJS tets that integrate well with CI tools:

* Unit Testing with Karma
* End-to-end (E2E) with Protractor

### Continnous Integration (CI)

CI tools (such as Travis CI or Jenkins) have the ability to run test scripts during build process and give immediate feedback by way of tests resuls.

### Testing Considerations

The two most popular test frameworks used for client-side Javascript and AngularJS, Karma and Protractor, run on the Node.js framework. Applications and test scripts that run on Node.js run extremely fast.

## Essential Modules

* angular.min.js (main)
* angular-route.min.js (routing)
* angular-cookies.min.js (cookies)
* angular-resource.min.js (REST)

## Controllers

AngularJS controllers have two primary duties in an application:

* Controllers should be used to initialize the model scope properties. When a controller is created and attached to the DOM, a child scope is created. **The child scope holds a model used specifically for the controller which is attached**. You can access the child scope by using the *$scope* object.
* Controllers add behavior to the *$scope* object. We add behavior by adding methods to the scope.

### Business Logic

Business logic that needs to be available to multiple controllers should not be placed in the controller but should instead be placed in AngularJS non-REST services.

```javascript
angular.module('addonsControllers',[])
    .controller('AddonsCtrl',['$scope','checkCreds','$location','AddonsList','$http','getToken',function AddonsCtrl($scope, checkCreds, $location, AddonsList, $http, getToken){
        if(checkCreds !== true){
            $location.path('/loginForm');
        }

        $http.defaults.headers.common['Authorization'] = 'Basic ' + getToken();

        AddonsList.getList({},
            function success(response){
                console.log("Success");
            },
            function error(errorResponse){
                console.log("Error");
            }
        );

        $scope.addonsActiveClass = "active";
    }]);
```

## Rest Services

Any business logic that can be pushed off the client-side application should be implemented as a **REST service** and not actually inside the AngularJS application.

**REST services** must have a response time of **two (2) seconds** or less.
