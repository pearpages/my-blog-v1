## What is Ionic?

+ Open source framework, mobile-optimized library for HTML/JS/CSS
+ Built on top of AngularJS
+ Built for native Cordova apps
+ "Bootstrap for mobile"

## Getting Started

### Command Line Features

$ start 
$ serve
$ platform
$ build
$ emulate
$ run

### Installing Ionic

We need *node.js*
$ npm cache clear

**install ionic**
$ sudo npm install ionic -g

**install cordova**
$ sudo npm install cordova -g

### Starting a New Project

$ ionic start [appname] [template]
$ ionic start based blank

### Run Ionic

**in the browser**
$ ionic serve

**emulating**
$ ionic build ios
$ ionic emulate ios

**in the device**
$ ionic run ios

### Ionic Templates

+ Blank
+ Tabs
+ Side Menu
+ Maps

$ ionic start tabsApp tabs
$ ionic start esApp sidemenu

## Navitation And Routing

+ Headers and Footers
+ Tabs
+ Side Menu
+ Routing

### Ionic Headers And Footers

<ion-header-bar class="bar-positive">
      <h1 class="title">Whatever</h1>
</ion-header-bar>

    <ion-content>
    </ion-content>

    <div class="bar bar-footer bar-positive">
      <div class="title">My Footer</div>
    </div>

### Ionic Tabs

<ion-tabs class="tabs-energize tabs-icon-top">
    <ion-tab title="Dashboard" icon="ion-home" href="#"></ion-tab>
    <ion-tab title="Dashboard" icon="ion-star" href="#"></ion-tab>
    <ion-tab title="Dashboard" icon="ion-gear-a" href="#"></ion-tab>
</ion-tabs>

[http://ionicons.com](http://ionicons.com)

### Angular UI Router

+ Routic framework for AngularJS
+ Organize into State Machines
+ Allows for Nested Views
+ 3 Ways to Activate a State
  + ui-serf
  + url
  + $state.go()

### State

+ Unique name
+ URL (Supports parameters)
+ Template / TemplateUrl
+ Controlelr (optional)

$stateProvider.state("contacts",{
   url: "/contacts",
   tempalteUrl: "contacts.html" 
});

### Nestet States/Views

+ Angular UI Router Supports Nested States
+ Ues Dot Notation
+ Child Inhierits from Parent (URL)
+ Abstract
  + Can have child states but not get activated itself
  + Must contain their own <ui-view/> (<ion-nav-view/>)

**code example** 
$stateProvider
    .state("foo", {
        abstract: true,
        url: "/foo",
        templateUrl: "foo.html" // must contain <ui-view/>
    })
    .state("foo.bar",{
        url: "/bar", //will be "foo/bar",
        templateUrl: "bar.html"
    })
    .state("foo.baz", {
        url: "/xxx", //will be "/foo/xxx"
        templateUrl: "baz.html"
    });

### Activating States

+ <a href="#/foo/bar">Go</a>
+ <a ui-sref="foo.bar">Go</a>
+ $state.go("foo.bar")

### Animations

<ion-nav-view name="mainContent" animation="slide-left-right"></ion-nav-view>

###  Button Back

<ion-nav-back-button class="button-clear button-icon icon ion-ios7-arrow"></ion-nav-back-button>

## Ionic Components

+ Lists
+ Grid System
+ Cards
+ Toggles and Buttons
+ Ionic Popup

### Lists

<div class="list">
      <a class="item" ng-repeat="league in leagues.leagues">{{league.name}}</a>
    </div>
