---
layout: post
title:  "Yeoman Angular Generators"
date:   2015-05-15 11:33:15
categories: yeoman javascript angularjs
---

Available generators:

* [angular](#app) (aka [angular:app](#app))
* [angular:controller](#controller)
* [angular:directive](#directive)
* [angular:filter](#filter)
* [angular:route](#route)
* [angular:service](#service)
* [angular:provider](#service)
* [angular:factory](#service)
* [angular:value](#service)
* [angular:constant](#service)
* [angular:decorator](#decorator)
* [angular:view](#view)

## App
Sets up a new AngularJS app, generating all the boilerplate you need to get started. The app generator also optionally installs Bootstrap and additional AngularJS modules, such as angular-resource (installed by default).

Example:
{% highlight bash %}
yo angular
{% endhighlight %}

## Route
Generates a controller and view, and configures a route in `app/scripts/app.js` connecting them.

Example:
{% highlight bash %}
yo angular:route myroute
{% endhighlight %}

Produces `app/scripts/controllers/myroute.js`:
{% highlight javascript %}
angular.module('myMod').controller('MyrouteCtrl', function ($scope) {
  // ...
});
{% endhighlight %}

Produces `app/views/myroute.html`:
{% highlight html %}
<p>This is the myroute view</p>
{% endhighlight %}

**Explicitly provide route URI**

Example:
{% highlight bash %}
yo angular:route myRoute --uri=my/route
{% endhighlight %}

Produces controller and view as above and adds a route to `app/scripts/app.js`
with URI `my/route`

## Controller
Generates a controller in `app/scripts/controllers`.

Example:
{% highlight bash %}
yo angular:controller user
{% endhighlight %}

Produces `app/scripts/controllers/user.js`:
{% highlight javascript %}
angular.module('myMod').controller('UserCtrl', function ($scope) {
  // ...
});
{% endhighlight %}

## Directive
Generates a directive in `app/scripts/directives`.

Example:
{% highlight bash %}
yo angular:directive myDirective
{% endhighlight %}

Produces `app/scripts/directives/myDirective.js`:
{% highlight javascript %}
angular.module('myMod').directive('myDirective', function () {
  return {
    template: '<div></div>',
    restrict: 'E',
    link: function postLink(scope, element, attrs) {
      element.text('this is the myDirective directive');
    }
  };
});
{% endhighlight %}

## Filter
Generates a filter in `app/scripts/filters`.

Example:
{% highlight bash %}
yo angular:filter myFilter
{% endhighlight %}

Produces `app/scripts/filters/myFilter.js`:
{% highlight javascript %}
angular.module('myMod').filter('myFilter', function () {
  return function (input) {
    return 'myFilter filter:' + input;
  };
});
{% endhighlight %}

## View
Generates an HTML view file in `app/views`.

Example:
{% highlight bash %}
yo angular:view user
{% endhighlight %}

Produces `app/views/user.html`:
{% highlight html %}
<p>This is the user view</p>
{% endhighlight %}

## Service
Generates an AngularJS service.

Example:
{% highlight bash %}
yo angular:service myService
{% endhighlight %}

Produces `app/scripts/services/myService.js`:
{% highlight javascript %}
angular.module('myMod').service('myService', function () {
  // ...
});
{% endhighlight %}

You can also do `yo angular:factory`, `yo angular:provider`, `yo angular:value`, and `yo angular:constant` for other types of services.

## Decorator
Generates an AngularJS service decorator.

Example:
{% highlight bash %}
yo angular:decorator serviceName
{% endhighlight %}

Produces `app/scripts/decorators/serviceNameDecorator.js`:
{% highlight javascript %}
angular.module('myMod').config(function ($provide) {
    $provide.decorator('serviceName', function ($delegate) {
      // ...
      return $delegate;
    });
  });
{% endhighlight %}