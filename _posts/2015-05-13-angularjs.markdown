---
layout: post
title:  "AngularJs"
categories: angularjs web javascript
date:   2015-05-13 19:32:53
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Javascript client-side frameworks are sustainable models that offer many advantages over conventional web frameworks, such as simplicity, rapid development, speed of operation, testability, and the ability to package the entire application and deploy it to all movile devices and the Web with relative ease.

## MVC

AngularJS uses the MVC design pattern and embraces that pattern completely. The model, view, and controller are all clearly defined in AngularJS.

Business logic should almost always be placed in backend REST services whenver possible.

## RESTful web services

AngularJS's **resource** object lets developers interact with  REST services like standard objects.

AngularJS services help to greatly simplify an application by compartmentalizing client-side logic into single units of code.

## Dependency Injection

Dependency injection (DI) is a design pattern where dependencies are defined in an application as part of the configuration. Dependency injection helps you avouid having to manually create application dependencies.

One of its main advantages is that it reduces the need for boilerplate code, writing of which would normally be a time-consuming proccess.

DI also helps to mak an application more testable.

## Testing

There are two types of AngularJS tets that integrate well with CI tools:

* Unit Testing with Karma
* End-to-end (E2E) with Protractor

### Continnous Integration (CI)

CI tools (such as Travis CI or Jenkins) have the ability to run test scripts during build process and give immediate feedback by way of tests resuls.

## Essential Modules

* angular.min.js (main)
* angular-route.min.js (routing)
* angular-cookies.min.js (cookies)
* angular-resource.min.js (REST)

