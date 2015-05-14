---
layout: post
title:  "AngularJS Security"
date:   2015-05-15 15:24:12
categories: security javascript angularjs
---

Security should always be implemented on the backend services where the data resides. That is the only safe place to implement security layer.

The following rules should be considered

* Always use some type of authentication on each REST service that contains private data.
* Always sue SSL to communicate with REST services that contain private data (HTTPS)
* Never implement a **Cross-Origin Resource Sharing (CORS) layer** that returns * as the list of allowed domains.
* Always make sure that any Javascript that may get injected inside a JSON property does not get executed server side.

The responsibility for security rests entirely on the shoulders of the backend service developers.
