---
layout: post
sidebar-align: left
title: "Communicating with the server with Angular"
categories: javascript rest http angular
date:  2016-03-13 08:12:23
author: Pere Pages
---

* TOC
{:toc}

$http is low level and *$resource is high level and for Restful End Points*.

## $resource (ngResource)

We can use $resource for get calls that not are necesseraly *resourceful*.

The next example does server side logic in the client side, it is **Bad practice**. It is just an example.

Add the .js file

```html
<script type="text/javascript" src="vendor/angular-resource.min.js"></script>
```

Add the dependency to the Module

```javascript
var app = angular.module('app',['ngResource']);
```

Factories and Service

```javascript
app.factory('users', function ($resource) {
    return $resource('/data/users/:id', {id: "@id"});
});
```

```javascript
app.factory('catalog', function ($resource) {
    return $resource('/data/courses/:id', {id: "@id"});
});
```

```javascript
// one Singleton to keep the User
app.value('identity', {});
```

Controllers

```javascript 
function LoginController (users,notifier,identity) {
    users.query().$promise.then(function(userCollection) {
        // userCollection is a simple Array
        userCollection.forEach(function (user) {
            if(name === user.name && password === user.password) {
                notifier.notify('You have successfully signed in!');
                identity.currentUser = user;
            }
        });
        if(identify.currentUser === undefined) {
            notifier.notify('Username/Password Combination incorrect');
        }
    });    
}
```

```javascript
function CatalogListController (catalog) {
    var vm = this;

    this.catalog = catalog.query();
}
```

```javascript
function CatalogController (catalog,notifier) {
    var vm = this;

    this.registerCourse = function (course) {
        course.registered = true;
        course.$save();
        notifier.notify('You have registered for '+ course.name);
    }
}
```

## $http

```javascript
app.factory('followedInstructors', function ($http) {
    return {
        get: function() {
            // ...
        },
        save: function() {
            // ...
        }
    };
});
```

## $http to READ

```javascript
app.factory('followedInstructors', function ($http, $q) {
    return {
        get: function() {
            // Solution1: This solution returns a promise
            // return $http.get('data/userData/followedInstructors');
            
            // Solution2: Also returns a promise but we move all the logic to the service
            var dfd = $q.defer();
            $http.get('data/userData/followedInstructors')
            .success(function (data) {
                dfd.resolve(data);
            });

            return dfd.promise;
        },
        save: function() {
            // ...
        }
    };
});
```

Controller

```javascript
function myController() {
    var vm = this;

    // Solution1: we use the success method of the promise
    // followedInstructors.get().success(function(data) {
    //      vm.followedInstructors = data;
    // });
    
    // Solution2
    vm.followedInstructors = follwedInstructors.get();
}   
```

## $http to SAVE

```javascript
app.factory('followedInstructors', function ($http) {
    return {
        get: function() {
            // ...
        },
        save: function(list) {
            $http.post('data/userData/followedInstructors', list)
        }
    };
});
```

## $resource with non Restful End Points

Usutally it isn't a good idea to use $resource for not Restful End Points, but we can still use it if we are using a GET.

```javascript
return $resource('data/userData/followedInstructors',undefined {
    get: {method: "GET", isArray: true}
}).get().$promise;
```

## Comparing promises from $http, $request and $q

### $http

Returns a Promise

**Methods**

* then (config)
* catch
* finally
* success (data,status,header,config)
* error

To access data with the *then* method we have to use *config.data*.

### $q

Returs a promise

**Methods**

* then (data)
* catch
* finally

### $resource

returns an Array

All the data, plus to additional objects $promise and $resolved.

```javascript
[$promise,$resolved]

// promise has another array with the elements, the $promise and boolean $resolved
```

## $http configuration

```javascript
return $http.get('data/userData/followedInstructors', {cache:true});
```

```javascript
$http.post('data/userData/followedInstructors', list, {headers: {"ContentType": 'application/x-www-form-urlencoded'}
});
```

### Configuring the App to have a default $http configuration

```javascript
angular.module('app',[])
.config(function ($httpProvider) {
    $httpProvider.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
});
```

## $http Transforms

Angular, for instance, has Transforms that do JSON serialization and deserialization for you automatically.

### Transform Request

```javascript
// Doing it this way my transformRequest goes first and then applies the rest of the default transformRequests.
$http.post('data/userData/followedInstructors', list, {
    transformRequest: [
        function (data, headersGetter) {
            // to inspect the headers we have to call the headersGeterr function
            // var headers = headersGetter();
            
            for (var i = 0; i<data.length; i++) {
                var item = data[i];
                item.ts = new Date();
            }
            return data;
        }
    ].concat($http.defaults.transformRequest);
});
```

### Transform Response

```javascript
// here the aprroach it's just the opposite, we put our changes the last.
return $http.get('data/userData/followedInstructors', {
    transformRespone : 
        $http.defaults.transformResponse.concat([
            function(data,headersGetter) {
                return data.followedInstructors;
            }
        ]);
    });
```

## Interceptors

Interceptors are very useful, for example, for Authentication tokens, or any thing that we need to add to each call.

We create the in the .config function and use the **$provide**. 

Interceptors have 4 different methods:

* request
* requestError
* response
* responseError

```javascript
angular.module('app',[])
.config(function($httpProvider, $provide) {
    $provide.factory('myInterceptor', function() {
        return {
            response: function (config) {
                if(config.config.url === '/data/courses') {
                    config.data.splice(5);
                }
                return config;
            }
        };
    });

    $httpProvider.interceptors.push('myInterceptor');
});
```

## Restangular

* It's a substitute for $resource.
* It has a dependency with *lodash*.
* You give it fragments of the URL and constructs the URL for you

```javascript
app.config(function(RestangularProvider) {
   Restangular.setBaseUrl('/data'); 
});
```

```javascript
app.factory('users',function(Restangular) {
    return Restangular.all('users');
});
```

```javascript
function myController(users) {
    users.getList().then(function(usersList) {
        // do whatever
        });
    users.one(1).get(1).then(function (){});
    uers.get(1);
    users.one(1).all('followedInstructors').getList();
}
```
