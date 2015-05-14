---
layout: post
title:  "AngularJs Routing"
categories: angularjs web javascript
date:   2015-05-14 11:12:53
---

Simple example about routing and vars through the url.

## app.js

Check the  **.when('/added-user/:user/:city'**

{% highlight javascript %}
//app.js
angular.modlule('routerApp',['ngRoute'])
    .config(['$routeProvider','$locationProvider',function($routeProvider,$locationProvider){
        $routeProvider
            .when('/',{
                templateUrl: 'views/main.html',
                controller: 'MainCtrl'
            })
            .when('/user',{
                templateUrl: 'views/user.html',
                controller: 'UserCtrl'
            })
            .when('/added-user/:user/:city',{
                templateUrl: 'views/added-user.html',
                controller: 'AddedUserCtrl'
            });
    }]);
{% endhighlight %}

## controllers.js 

Pay attention to the **$routeParams**

{% highlight javascript %}
//controllers.js
angular.module('routerApp',[])
    .controller('AddedUserCtrl',['$scope','$routeParams', function($scope,$routeParams){
        
        $scope.name = $routeParams.name;
        $scope.city = $routeParams.city;

    }]);
{% endhighlight %}

## added-user.html

{% highlight html %}
//added-user.html
<div>User: {{name}}</div>
<div>City: {{city}}</div>
{% endhighlight %}

