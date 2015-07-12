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
