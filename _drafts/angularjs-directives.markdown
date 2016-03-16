---
layout: post
title:  "Angular Directives"
date:   2015-06-22 19:48:12
categories: angularjs directives
---
## Main Concepts

### What can directives do?

* Manipulate the DOM
* Iterate through data
* Handle events
* Modify CSS
* Validate data
* Data binding

### General types

* Forms
        + ng-maxlength
        + ng-minlength
        + ng-pattern
        + ng-required
        + ng-submit
* Behavior
        + ng-blur
        + ng-change
        + ng-checked
        + ng-click
        + ng-key
        + ng-mouse
* Data Binding
        + ng-bind
        + ng-href
        + ng-init
        + ng-model
        + ng-src
        + ng-style
* Application
        + ng-app
        + ng-controller
* DOM
        + ng-disabled
        + ng-cloak
        + ng-hid
        + ng-if
        + ng-repeat
        + ng-show
        + ng-switch
        + ng-view

### 3rd Party Directives

* UI Bootstrap
* AngularStrap
* Angular UI Grid
* Angular Translate

### Directives categories

* DOM-Driven Directives: All about DOM Manipulation
* Data-Driven Directives: All about data, using other directives and a controller. The equivalent of a view with a controller (Baby view).
* Behavior-Driven Directives: All about handling DOM Events.

### Directive Types

* Attribute directives: <span hello-world></span>
* Element directives: <hello-world></hello-world>
* CSS class directives: <span class="hello-world: exp;"></span>
* Comment directives: <!-- directive: hello-world exp --> 

### $compile

$compile > DDO (Directive Definition Object) > template > scope

Template --> $compile --> Template function |--> <html>
                      --> Scope             |

### Directive Definition Object (DDO)

* Defines the template for the directive
* Can include DOM manipulation code
* Can define a controller for the directive
* Controls the directive's scope
* Defines how the directive can be used

#### Properties

* restrict
* template
* templateUrl
* scope
* controller
* link

## Shared and Isolate Scope

### Shared Scope

Shared Scope is the inherited scope. And they behave the same way that controllers do. They are inherited in a prototypical way.

**Controller** 

$scope.customers = [];

**Directive**

$scope.customers = [];

Because the variable it is already defined in the controller we inherit it.

$scope.isolated = true;

Because the variable has a different name, it is isolated.

### Isolate Scope

There's a way to communicate with the outside but it's isolated.

* @ Local Scope Property: One-way binding (entry)
* = Local Scope Property: Two-way binding
* & Local Scope Property: Parent Scope with Function Callback

## The link() Function

The link function it's about DOM manipulation.

<% highlight js %>
return {
        link: function (scope, element, attr) {}
};
<% endhighlight %>

Angular by default has already a jqLite so you do not really need jQuery.

###jqLite typical Functions

[jqLite Docs](https://docs.angularjs.org/api/ng/function/angular.element)

angular.element()
addClass()/css()
attr()
on()/off()
find()
append()/remove()
html()/text()
ready()

## Automate templateUrl

(function(currentScriptPath) {
    'use strict';

    angular.module("mandatory")
        .directive('dropdownButton', ['$sce',dropdownButton]);

    function dropdownButton($sce) {
        return {
            restrict: 'E',
            bindToController: true,
            controllerAs: 'vmd',
            controller: controller,
            scope: {
                options: '=',
                current: '=',
                onMyChange: '&'
            },
            templateUrl: currentScriptPath.replace('dropdown-button.directive.js', 'dropdown-button.html'),
        };

        //call ang-link if needed

        function controller() {

            var vmd = this;
            vmd.render = render;
            vmd.changeValue = changeValue;

            function render(html) {
                return $sce.trustAsHtml(html);
            }

            function changeValue(value) {
                vmd.onMyChange({value:value});
            }
        }
    }
})((function currentScriptPath() {
    var scripts = document.getElementsByTagName("script");
    var currentScriptPath = scripts[scripts.length - 1].src;
    return currentScriptPath;
})());

