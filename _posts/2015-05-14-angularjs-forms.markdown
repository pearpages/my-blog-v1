---
layout: post
title:  "AngularJS Forms"
date:   2015-05-14 11:00:00
categories: javascript angularjs
---

## The Form

### Directives

* ng-submit
* ng-model

Two or more controllers can be applied to the same element, and we can use **controller as** to identify each controller.

{% highlight html %}
<form ng-submit="user.submit()" ng-controller="AddUserCtrl as user">
    
    <div>
        <input type="text" ng-model="user.name" required />
    </div>

    <div>
        <input type="text" ng-model="user.city" required/>
    </div>

    <div>
        <button type="submit">Add Customer</button>
    </div>

</form>
{% endhighlight %}

## The Controller

{% highlight javascript %}
app.controller('AddUserCtrl',['$scope','$location',function($scope,$location){
    $scope.sumbit = function(){
        $location.path('/addedUser/' + $scope.name + '/' + $scope.city);
    };
}]);
{% endhighlight %}