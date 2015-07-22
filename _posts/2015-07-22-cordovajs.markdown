---
layout: post
title:  "CordovaJs"
date:   2015-07-22 19:33:15
categories: javascript cordovajs
---

## Introduction

Apache Cordova is an open-source mobile development framework. It allows you to use standard web technologies such as HTML5, CSS3, and JavaScript for cross-platform development, avoiding each mobile platforms' native development language.

Applications execute within wrappers targeted to each platform.

## Summary

1. cordova create hello com.example.hello HelloWorld
2. cordova platform add ios
3. cordova plugin add cordova-plugin-device
4. cordova build
5. cordova emulate ios

When adding a platform the /www folder will get copied to each platform.
When we build, we actually do it for all the platforms installed.

### Basic Components

Apache Cordova applications rely on a common **config.xml** file that provides information about the app and specifies parameters affecting how it works, such as whether it responds to orientation shifts. This file adheres to the **W3C's Packaged Web App**, or **widget**, specification.

A plugin interface is available for Cordova and native components to communicate with each other. This enables you to invoke native code from JavaScript.

### Development Paths

* Cross-platform (CLI) workflow
* Platform-centered workflow

## The Command-Line Interface

1. Download and install **Node.js**
2. Download and install a **git client**
3. Install cordova: $ *sudo npm install -g cordova*

### Create the app

{% highlight bash %}
$ cordova create hello com.exeample.hello HelloWorld -d
# -d is for showing the progress
# hello is the folder that should not exist
# com.example.hello provides the project with a reverse domain-style identifier
# HelloWorld is the application display title
{% endhighlight %}

Its *www* subdirectory hosues the application's home page, along with various resources (css,js, img, ...). These assets will be stored on the device's local filesystem, not served remotely.

The **config.xml** file contains important metadata needed to generate and distribute the application.

## Add platforms

These commands affect the *platforms* directory.

{% highlight bash %}
$ cordova platform add ios

$ cordova platform ls
# to check the current platforms
{% endhighlight %}

The **www source** directory is reproduced (copied) within each platform's subdirectory, appearing for example in platforms/ios/www or platforms/android/assets/www. 

Because the CLI constantly copies over files from the source www folder, you should only edit these files and not the ones located under the platforms subdirectories.

The files in this directory are routinely overwritten when preparing applications for building, or when plugins are reinstalled.

## Build the app

By default, the cordova create script generates a skeletal web-based application whose home page is the project's **www/index.html** file. 
Edit this application however you want, but any initialization should be specified as part of the **deviceready event handler**, referenced by default from www/js/index.js.

{% highlight bash %}
$ cordova build
{% endhighlight %}

## Emulate 

{% highlight bash %}
# you have to previously do the installation and config
$ cordova emulate ios
{% endhighlight %}

## Add Plugin Features

> A plugin is a bit of add-on code that provides an interface to native components. 

As of version 3.0, when you create a Cordova project it does not have any plugins present. 
This is the new default behavior. **Any plugins** you desire, even the core plugins, must be **explicitly added**.

[List of plugins (plugins.cordova.io*)](http://plugins.cordova.io/#/)

### Operations with plugins

{% highlight bash %}
# search
$ cordova plugin serach bar code

# add
$ cordova plugin add cordova-plugin-device

# list installed plugins
$ corodova plugin ls

# remove
$ cordova remove cordova-plugin-device

# update
# for updating a plugin you are supposed to remove it first, and then add it again.

# advanced
$ cordova plugin add cordova-plugin-console@latest
$ cordova plugin add cordova-plugin-console@0.2.1
$ cordova plugin add https://github.com/apache/cordova-plugin-console.git
$ cordova plugin add https://github.com/someone/aplugin.git#:/my/sub/dir
{% endhighlight %}

## Help commands

{% highlight bash %}
$ cordova help
$ cordova # same

# more detailed info on a specific command
$ cordova run --help

# info about the cordova installed
$ cordova info
{% endhighlight %}

## Updating Cordova

{% highlight bash %}
$ sudo npm update -g cordova

# specific version
$ sudo npm install -g cordova@3.1.0-0.2.0

# current installed
$ npm info cordova
$ cordova -v
{% endhighlight %}