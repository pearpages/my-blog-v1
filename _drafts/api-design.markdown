---
layout: post
title: "Web Api Design"
categories: api design
date:  2016-03-01 19:40:22
---

#### Contents
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Introduction

### Api Ecosystem

#### HTTP / RPC

+ *Verbs Included in API*
+ URI Endpoints

#### Restful

Stateless

+ URI Endpoints
+ *Resource URIs*
+ *HTTP Verbs*
+ *Stateless Server*
+ *Content Negotiation*

#### HATEOAS

> Hipermedia as the engine of application state.

+ Resource URIs
+ HTTP Verbs
+ Stateless Server
+ Content Negotiation
+ *Link Relations*

### Resource Based Architectures

* Resources are representations of Real Wolrd *Entities* (People, Invoices, Payments, ...)
  * Relationships are typically nested
  * Hierarchies or Webs, **NOT Relational Models**

