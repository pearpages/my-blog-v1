---
layout: post
title: "title"
categories: category1 category2
date:  2015-05-26 19:40:22
---

#### Contents
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}


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

### List Dividers

<div class="list">
      <div ng-repeat="division in teams.teams">
      <div class="item item-divider item-energized">{{division.divisionName}}</div>

        <a class="item item-icon-right" ng-repeat="team in division.divisionTeams" href="#app/teams/{{team.id}}">{{team.name}}
        <i class="icon icon-chevron-right icon-accessory"></i></a>
      </div>
    </div>


Another Example

<div class="list">
      <div ng-repeat="division in standings.standings">
        <div class="item item-divider item-energized">{{division.divisionName}}</div>

        <a href="#/app/teams/{{team.id}}" class="item item-icon-right" ng-repeat="team in division.divisionStandings">
          {{team.teamName}} ({{team.wins}}-{{team.losses}})
          <i class="icon icon-chevron-right icon-accessory"></i>
        </a>
      </div>
    </div>

### Ionic Grids

Uses Flexbox

+ Responsive
+ Supports Explicit Column Sizes
+ Supports Column Offsets
+ Control of Vertical Alignment

**example**

<div class="row">
        <div class="col-20">
          <p>{{game.time | date:'M/d/yy'}}</p>
          <p>{{game.time | date: 'shortTime'}}</p>
        </div>

        <div class="col col-center">
          <h3>{{game.homeAway}} {{game.opponent}}</h3>
          <p>{{game.location}}</p>
        </div>
        <div class="col-20">
          <h4 class="positive">{{game.scoreDisplay}}</h4>
        </div>          
      </div>

### Ionic Cards

<div class="card">
      <div class="item item-divider item-energized">
        Home Team
      </div>
      <a class="item item-text-wrap item-icon-right" ng-href="#/app/teams/{{game.game.team1Id}}">
        {{game.game.team1}}
      </a>
      <div class="item item-divider">
        Score: {{game.game.team1Score}}
      </div>
    </div>

### Ionic Toggle Controls

<div class="item item-checkbox">
      <h2>{{teamDetail.following ? "Following" : "Not Following"}}</h2>
      <label class="checkbox">
        <input type="checkbox" ng-model="teamDetail.following">
      </label>
    </div>

    <div class="item item-checkbox">
      <h2>{{teamDetail.following ? "Following" : "Not Following"}}</h2>
      <label class="toggle toggle-energized">
        <input type="checkbox" ng-model="teamDetail.following">
        <div class="track">
          <div class="handle"></div>
        </div>
      </label>
    </div>

### Ionic Popup

function toggleFollow(){
      if(vm.following){
        var confirmPopup = $ionicPopup.confirm({
          title: "Unfollow?",
          template: 'Are you sure you want to unfollow?'
        });
        confirmPopup.then(function(res){
          if(res){
            vm.following = !vm.following;
          }
        });
      }else{
        vm.following = !vm.following;
      }
    }

## Data and Caching

+ HTTP
+ Promises
+ Loading
+ Caching (also off line escenarios)
+ Refreshing (pulling and releasing)

## Using $http

function getLeagues(callback){
        $http.get('http://elite-schedule.net/api/leaguedata')
          .success(function(data){
            callback(data);
          });
    }

### Using $q (promises)

function getLeagues(){
      var deferred = $q.defer();

        $http.get("http://elite-schedule.net/api/leaguedata")
          .success(function(data){
            deferred.resolve(data);
          })
          .error(function(){
            console.log("Error while making HTTP call.");
            deferred.reject();
          });

          return deferred.promise;
    }


### $ionicLoading

function getLeagues(){
      var deferred = $q.defer();


      $ionicLoading.show({
        template: "Loading..."
      });

        $http.get("http://elite-schedule.net/api/leaguedata")
          .success(function(data){
            $ionicLoading.hide();
            deferred.resolve(data);
          })
          .error(function(){
            console.log("Error while making HTTP call.");
            $ionicLoading.hide();
            deferred.reject();
          });

          return deferred.promise;
    }

    ### Angular Cache

+ Angular-cache replacement for Angular's **$cacheFactory**
+ Configurable TTL
+ Configurable Storage Options (e.g., Local Storage)
+ Expiration Events

### Manually Refreshing Data
