---
layout: post
sidebar-align: left
title:  "AngularJS Services"
date:   2015-05-14 15:30:25
categories: web javascript angularjs
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Three ways

* service
* provider
* factory

The **factory** way is the most commonly used method.

```javascript
angular.module('someServices',['ngResource'])
    .service('serviceLorem',[...])
    .provider('providerLorem',[...])
    .factory('factoryLorem'[...])
```

## Business Logic

Services can contain buesiness logic that is used by multiple controllers.

For example, a situation where a user needs to authenticate across multiple REST services. One way to do that is by using Basic Authentication, where the username's and password are passed to a service as a token in the HTTPS header during the service call.

Once a user makes a call to the login service and the user's credentials are validated, it is the job of the AngularJS application to temporarily store those credentials. 

It is also the job of the AngularJS application to direct the user to a login page when the user has not autenticated.

## Communicating with REST Services

* $http service
* $resource object

### $resource

The $resource object is by far the easiest way to call REST services.

```javascript
'use strict';

    angular.module('myApp',[])
        .factory('myFactory',['$resource',function($resource){
            return $resource("http://mybackend.com/rs/data", {}, {
            get: {method: 'GET', cache:false, isArray:false},
            save: {method: 'POST', cache:false, isArray:false},
            update: {method: 'PUT', cache:false, isArray:false},
            delete: {method: 'DELETE', cache:false, isArray:false}
            });
        }]);
```

## Controller

Theoretically we don't know when the REST service call will return results, but when it does, either the success callback function or the error callback function will be called.

```javascript
    angular.module('myApp',[])
        .controller('myController',['$scope','$routeParams','myFactory',function($scope,$routeParams,myFactory){
            var id = $routeParams.id;

            myFactory.get({id: id}, 
                function success(response){
                    console.log("Success: " + JSON.stringify(response));
                    $scope.element = response;
                },
                function error(errorResponse){
                    console.log("Error: " + JSON.stringify(errorResponse));
                }
            );
        }]);

```

## Other Examples

```javascript
angular.module('myModule',[])
    .factory('User',['$resource',function ($resource){
        return $resource("./server/user/:id", {},{
        get: {method: 'GET', cache: false, isArray: false},
        save: {method: 'POST', cache: false, isArray: false},
        update: {method: 'PUT', cache: false, isArray: false},
        delete: {method: 'DELETE', cache: false, isArray: false}
        });
    }]);
```

```javascript
angular.module('myModule',[])
    .factory('UserList',['$resource',function ($resource){
        return $resource("./server/userList", {},{
        get: {method: 'GET', cache: false, isArray: true}
    });
    }]);
```

```javascript
angular.module('myModule',[])
    .factory('User',['$resource',function ($resource){
        return $resource("./server/login", {}, {
        login: {method: 'POST', cache: false, isArray: false}
        });
    }]);
```
