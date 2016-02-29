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
* Resources are represented in URIs
  *	Query strings for non-data elements (eg. format, sorting, etc)

### REST

> REpresentational State Transfer

* Seperation of Client and Server
* Server Requests are Stateless
* Cacheable Requests 
* Uniform Interface

### Hypermedia

* Method of self-describing messages
  * Links in resources that describe how to process data
  * Hyperlinks for resources
* Hypermedia == HATEOAS
  * It can be very useful or just additional overhead, so it is only as important as we need it to be
  * Self-documenting APIs

## Desigining the API

### URI Design

* Nouns are Good, Verbs are Bad
  * Prefer Plurals (e.g.: Customers, Gaimes, Invoices)
* Use Identifiers to locate individual items in URIs
  * Does not have to be Internal Key... but it has to point to only one item.

#### Using Verbs

| Resource  | GET (read)  | POST (create)  | PUT (update)  | DELETE (delete)  |
|---|---|---|---|---|
| /customers | Get List | Create Item | Update Batch | Error |
| /customers/123 | Get Item| Error | Update Item| Delete Item |

#### Returning

| Resource  | GET (read)  | POST (create)  | PUT (update)  | DELETE (delete)  |
|---|---|---|---|---|
| /customers | List | New Item | Status Code Only | Status Code Only* |
| /customers/123 | Item| Status Code Only* | Updated Item| Satus Code Only |

#### Update Example

** Headers **

```
// Method PUT
User-Agent: Fiddler
Host: localhost:8863
Content-Type: application/json
```

** Request Body **

```
{"id":"1","name":"Pere Pages"}
```

** Response **

```
HTTP/1.1 200 OK
```

### Status Codes

| Code | Description | Code | Description |
|---|---|---|---|
| 200 | OK | 400 | Bad Request |
| 201 | Created | 401 | Not Authorized |
| 202 | Accepted | 403 | Forbidden |
| 302 | Found | 404 | Not Found |
| 304 | Not Modified | 405 | Method Not Allowed |
| 307 | Temp Redirect | 409 | Conflict |
| 308 | Perm Redirect | 500 | Internal Error |

* Use HTTP Status Codes (minimum 200,400,500)
  * 200 "It worked"
  * 400 "You did bad"
  * 500 "We did bad"
* Probably
  * 201 Created
  * 304 Not Modified
  * 404 Not Found
  * 401 Unauthorized
  * 403 Forbidden

### Associations