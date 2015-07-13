---
layout: post
title:  "AngularJS Forms"
date:   2015-05-14 11:00:00
categories: javascript angularjs
---

## The Form

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
### Directives

* ng-submit
* ng-model

#### ng-submit

Automatically prevents the brower from doing its defualt *METHOD* action when it tries to submit the form.

## The Controller

{% highlight javascript %}
app.controller('AddUserCtrl',['$scope','$location',function($scope,$location){
    $scope.sumbit = function(){
        $location.path('/addedUser/' + $scope.name + '/' + $scope.city);
    };
}]);
{% endhighlight %}

## Validate a form

Disable a button because the form is not valid

{% highlight javascript %}
<form name="addUserForm" ng-controller="myController">
...
<button ng-click="addUser()" ng-disabled="!addUserForm.$valid">Submit</button>
</form>
{% endhighlight %}

## $watch

When not only the users  update a particular input we might need to keep track of it.

You can call **$watch()** with an expression to observe and a callback that gets invoked whenever the expression changes.

{% highlight javascript %}
$scope.$watch('myObject.myValue', myCallback);

//$watch(watchFn, watchAction, deepWatch)
{% endhighlight %}

* watchFn
* watchAction
* deepWatch

#### watchFn

This parameter is a string with an Angular expression or a function that returns the current value of the model you want to watch.

#### watchAction

This is the function or expression to be called when the *watchFn* changes.

#### deepWatch

It tells Angular to examine each property within the watched object for changes.
