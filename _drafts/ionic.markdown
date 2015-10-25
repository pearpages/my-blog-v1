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

