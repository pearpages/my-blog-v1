---
layout: post
title:  "AngularJS Directives"
date:   2015-05-15 12:34:01
categories: directives javascript angularjs
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Directives are what sets AngularJS apart form Javascript client-side frameworks.

Examples of directives are *ngModel*, *ngView* or *ngRepeat*.

## AngularJS made directives

Some examples:

* ng-click
* ng-repeat
* ng-change (whenever the **USER** changes the value). See **$scope.$watch**.
* ng-show, ng-hide
* ng-class
* ng-src, ng-href

**ng-src** **ng-href**

Because Browsers ara agressive about loading images parallel to other content. Angular doesn't get a chance to intercept data binding requests.

**ng-class** examples

{% highlight html %}
<style>
    .warning{
        background-color: yellow;
    }
    .error{
        background-color: red;
    }
</style>

<div ng-controller ='myController'>
    <div ng-class="{error: isError, warning: isWarning}" ng-bind="messageText">
    </div>

    <button ng-click="showError()">Simulate Error</button>
    <button ng-click="showWarning()">Simulate Warning</button>
</div>
{% endhighlight %}

{% highlight javascript %}
function HeaderController($scope){
    $scope.isError = false;
    $scope.isWarning = false;

    $scope.showError = function (){
        $scope.messageText = 'This is an error!';
        $scope.isError = true;
        $scope.isWarning = false;
    };

    $scope.showWarning = function (){
        $scope.messageText = 'Just a warning. Please carry on.';
        $scope.isWarning = true;
        $scope.isError = false;
    };
}
{% endhighlight %}

## Creating Directives

### "Compiling"

AngularJS searches through the DOM tree to identify HTML elements associated with directives. The compiler then builds the template and assigns events to the associated elements in the template.

### Naming Conventions

HTML is case-insentive. We refer to a directive like *this-name* iin the template file and the AngularJS HTML compiler then normalizes the directive name into its *camel case* equivalent, *thisName*.

We use prefixes so our directives don't match any existing HTML tag name, future HTML tag name or AngularJS directives.

### Restrict Option

For e.g. myAppCalendar

* 'A' (attribute) <div my-app-calendar></div>
* 'E' (element) <my-app-calendar />
* 'C' (class name) <div class="my-app-calendar"></div>
* 'M' (comment name) <!-- directive: my-app-calendar -->

### Code Example

#### Directive
{% highlight javascript %}
angular.module('myApp')
  .directive('myMenu', function () {
    return {
      templateUrl: 'views/header.html',
      restrict: 'A',
      link: function postLink(scope, element, attrs) {
        scope.label = attrs.menuTitle;
    }};
  });
{% endhighlight %}

#### In the View
{% highlight html %}
<div blg-menu menu-title="AngularJS Blog"></div>
{% endhighlight %}
