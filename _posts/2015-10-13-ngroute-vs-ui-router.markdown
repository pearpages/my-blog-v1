---
layout: post
title:  "ngRoute vs ui-router"
date:   2015-10-13 18:12:43
categories: javascript angularjs routing
---

**ngRoute** merely allows you to assign controllers and templates to URL routes, whereas the fundamental abstraction in **ui-router** is **states**, which is a more powerful concept. 

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## ui-router feaures

ui-router is a 3rd-party module and is very powerful. It supports everything the normal ngRoute can do as well as many extra functions.

Here are some common reason ui-router is chosen over ngRoute:

+ Nested Views
+ Strong-type linking between states based on state names
+ Decorators
+ Map different information about different states
+ Easily determine if you are in a state or parent of a state

### Nested Views

It allows for [nested views](https://github.com/angular-ui/ui-router/wiki/Nested-States-%26-Nested-Views) and [multiple named views](https://github.com/angular-ui/ui-router/wiki/Multiple-Named-Views). This is very useful with larger app **where you may have pages that inherit from other sections**.

### Strong-type linking between states based on state names

It allows for you to have strong-type linking between **states based on state names**. Change the url in one place will update every link to that state when you build your links with **[ui-sref](http://angular-ui.github.io/ui-router/site/#/api/ui.router.state.directive:ui-sref)**. Very useful for larger projects where URLs might change.

### Decorators

There is also the concept of the **decorator** which could be used to allow your routes to be dynamically created based on the URL that is trying to be accessed. This could mean that you will not need to specify all of your routes before hand.

### Map different information about different states

[States](https://github.com/angular-ui/ui-router/wiki#state-manager) allow you to map and access different information about different states and you can easily pass information between states via **[$stateParams](https://github.com/angular-ui/ui-router/wiki/URL-Routing#stateparams-service)**.

### Easily determine if you are in a state or parent of a state

You can easily determine if you are in a state or parent of a state to adjust UI element (highlighting the navigation of the current state) within your templates via **[$state](http://angular-ui.github.io/ui-router/site/#/api/ui.router.state.$state)** provided by ui-router which you can expose via setting it in $rootScope on run.

## Links

[Github](https://github.com/angular-ui/ui-router)
Documentation:
[API Reference](http://angular-ui.github.io/ui-router/site/#/api)
[Guide](https://github.com/angular-ui/ui-router/wiki)
[FAQs](https://github.com/angular-ui/ui-router/wiki/Frequently-Asked-Questions)
[Sample Application](http://angular-ui.github.io/ui-router/sample/#/)
[Setting up the ui-router](http://www.ng-newsletter.com/posts/angular-ui-router.html)