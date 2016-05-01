---
layout: post
title:  "CordovaJs"
date:   2015-07-22 19:33:15
categories: javascript cordovajs
author: Pere Pages
---

## Introduction

Apache Cordova is an open-source mobile development framework. It allows you to use standard web technologies such as HTML5, CSS3, and JavaScript for cross-platform development, avoiding each mobile platforms' native development language.

Applications execute within wrappers targeted to each platform.

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Summary

There are two "paths" for developing an app with cordova:

+ The Command-Line Interface (CLI) way, which is multi-platform.
+ A platform-centered workflow

1. cordova create hello com.example.hello HelloWorld
2. cordova platform add ios
3. cordova plugin add cordova-plugin-device
4. cordova build
5. cordova emulate ios

When adding a platform the /www folder will get copied to each platform.
When we build, we actually do it for all the platforms installed.

## Basic Components

Apache Cordova applications rely on a common **config.xml** file that provides information about the app and specifies parameters affecting how it works, such as whether it responds to orientation shifts. This file adheres to the **W3C's Packaged Web App**, or **widget**, specification.

A plugin interface is available for Cordova and native components to communicate with each other. This enables you to invoke native code from JavaScript.

#### Core Components

* cordova CLI
* Embedded WebView
* Plugin Interface
* Storage

#### Third Party Components

* Accelerometer
* BatteryStatus
* Camera
* Capture
* Compass
* Connection
* Contacts
* Device
* Events
* File
* Fie Transfer
* Geolocation
* Globalization
* InAppBrowser
* Splashscreen
* Status Bar
* Vibration

### Development Paths

* Cross-platform (CLI) workflow
* Platform-centered workflow

## The config.xml

* Core Elements
* Global Preferences
* Multi-Platform Preferences
* Feature Element
* The Platform Element. 

#### Core Configuration Elements

* widget
* name
* description
* content
* access
* preference

```xml
<widget id="com.example.hello" version="0.0.1">
        <name>HelloWorld</name>
        <description>
            A sample Apache Cordova application that responds to the deviceready event.
        </description>
        <author email="dev@callback.apache.org" href="http://cordova.io">
            Apache Cordova Team
        </author>
        <content src="index.html" />
        <access origin="*" />
</widget>
```

#### 

## The Command-Line Interface

1. Download and install **Node.js**
2. Download and install a **git client**
3. Install cordova: $ *sudo npm install -g cordova*

### Create the app

```bash
$ cordova create hello com.exeample.hello HelloWorld -d
# -d is for showing the progress
# hello is the folder that should not exist
# com.example.hello provides the project with a reverse domain-style identifier
# HelloWorld is the application display title
```

Its *www* subdirectory hosues the application's home page, along with various resources (css,js, img, ...). These assets will be stored on the device's local filesystem, not served remotely.

The **config.xml** file contains important metadata needed to generate and distribute the application.

## Add platforms

These commands affect the *platforms* directory.

```bash
$ cordova platform add ios

$ cordova platform ls
# to check the current platforms
```

The **www source** directory is reproduced (copied) within each platform's subdirectory, appearing for example in platforms/ios/www or platforms/android/assets/www. 

Because the CLI constantly copies over files from the source www folder, you should only edit these files and not the ones located under the platforms subdirectories.

The files in this directory are routinely overwritten when preparing applications for building, or when plugins are reinstalled.

## Build the app

By default, the cordova create script generates a skeletal web-based application whose home page is the project's **www/index.html** file. 
Edit this application however you want, but any initialization should be specified as part of the **deviceready event handler**, referenced by default from www/js/index.js.

```bash
$ cordova build
```

## Emulate 

```bash
# you have to previously do the installation and config
$ cordova emulate ios
```

## Add Plugin Features

> A plugin is a bit of add-on code that provides an interface to native components. 

As of version 3.0, when you create a Cordova project it does not have any plugins present. 
This is the new default behavior. **Any plugins** you desire, even the core plugins, must be **explicitly added**.

[List of plugins (plugins.cordova.io*)](http://plugins.cordova.io/#/)

* **cross-platform workflow**, you use the cordova CLI utility to add plugins, as described in The Command-Line Interface. The CLI modifies plugins for all specified platforms at once.
* **platform-centered workflow**, you use a lower-level Plugman command-line interface, separately for each targeted platform.

[Plugman info](https://cordova.apache.org/docs/en/4.0.0/plugin_ref_plugman.md.html)

### Operations with plugins

```bash
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
```

## Help commands

```bash
$ cordova help
$ cordova # same

# more detailed info on a specific command
$ cordova run --help

# info about the cordova installed
$ cordova info
```

## Updating Cordova

```bash
$ sudo npm update -g cordova

# specific version
$ sudo npm install -g cordova@3.1.0-0.2.0

# current installed
$ npm info cordova
$ cordova -v
```

## Storage

#### Links
[HTML 5 Features Storage](http://www.html5rocks.com/en/features/storage)
[Exploring the FileSystem APIs](http://www.html5rocks.com/en/tutorials/file/filesystem/)

### Options

* LocalStorage
* WebSQL
* IndexedDB
* Plugin-Based Options
    + [File API](https://github.com/apache/cordova-plugin-file)
    + [Cordova plugins](http://plugins.cordova.io/#/)

#### LocalStorage

Also known as web storage, simple storage, or by its alternate session storage interface, this API provides synchronous key/value pair storage, and is available in underlying WebView implementations. Refer to the W3C spec for details.

#### WebSQL

**iOS** and **Android**

This API is available in the underlying WebView. The Web SQL Database Specification offers more full-featured database tables accessed via SQL queries.

#### IndexedDB

This API is available in the underlying WebView. Indexed DB offers more features than LocalStorage but fewer than WebSQL.

## iOS

### iOS WebViews

[This guide shows how to embed a Cordova-enabled WebView component within a larger iOS application](http://cordova.apache.org/docs/en/5.0.0/guide_platforms_ios_webview.md.html#iOS%20WebViews)

### iOS Plugins

Each plugin class **must be registered** as a <feature> tag in the named application directory's **config.xml** file.

Specify the plugin as a <feature> tag in your Cordova-iOS application's project's config.xml

```xml
<feature name="LocalStorage">
    <param name="ios-package" value="CDVLocalStorage" />
</feature>
```

### iOS Configuration

```xml
<preference name="EnableViewportScale" value="true"/>
<meta name='viewport' content='width=device-width, initial-scale=1, user-scalable=no' />
<preference name="MediaPlaybackRequiresUserAction" value="true"/>
<preference name="AllowInlineMediaPlayback" value="true"/>
<preference name="BackupWebStorage" value="local"/>
<preference name="TopActivityIndicator" value="white"/>
<preference name="KeyboardDisplayRequiresUserAction" value="false"/>
<preference name="SuppressesIncrementalRendering" value="true"/>
<preference name="GapBetweenPages" value="0"/>
<preference name="PageLength" value="0"/>
<preference name="PaginationBreakingMode" value="page"/>
<preference name="PaginationMode" value="unpaginated"/>
<preference name="UIWebViewDecelerationSpeed" value="fast" />
<preference name="ErrorUrl" value="myErrorPage.html"/>
```

### Deploy tools

```bash
$ npm install -g ios sim
$ npm install -g ios-deploy

# deploy the app on a connected iOS device:
$ cordova run ios --device
```

## The config.xml file

>  This platform-agnostic XML file is arranged based on the W3C's Packaged Web Apps (Widgets) specification, and extended to specify core Cordova API features, plugins, and platform-specific settings.

