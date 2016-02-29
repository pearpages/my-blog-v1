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
| /Customers | Get List | Create Item | Update Batch | Error |
| /Customers/123 | Get Item| Error | Update Item| Delete Item |

#### Returning

| Resource  | GET (read)  | POST (create)  | PUT (update)  | DELETE (delete)  |
|---|---|---|---|---|
| /Customers | List | New Item | Status Code Only | Status Code Only* |
| /Customers/123 | Item| Status Code Only* | Updated Item| Satus Code Only |

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
{"id":1,"name":"Pere Pages"}
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

* For sub-objects
  * Use URI Navigation ('http://myDomain.com/api/Customers/123/Invoices')
  * Should return a List of Related Objects or a Related Object
* May include multiple associtations on same object
  * 'http://myDomain.com/api/Customers/123/Invoices'
  * 'http://myDomain.com/api/Customers/123/Payments'
  * 'http://myDomain.com/api/Customers/123/Shipments'
* Anything more complex should use query string
  * 'http://myDomain.com/api/Customers?state=GA'
  * 'http://myDomain.com/api/Customers?state=GA&salesperson=144'
  * 'http://myDomain.com/api/Customers?hasOpenOrders=true'

### Formatting Results

* Content Negotiation is the Best Practice. Use Accept header to determine how to format.
* Use the URI components to format (not the best practice)
  * 'http://myDoomain/api/Customers?format=json'
  * 'http://myDoomain/api/Customers?format=jsonp&callback=foo'

** Accept Header **

```
GET /api/games2 HTTP/1.1
Accept: applications/json,text/xml
Host: localhost:8863
```

#### Content Types

| Type | MIME Type |
|---|---|---|
| JSON | application/json |
| XML | text/xml |
| JSONP* | applicaiton/javascript |
| RSS | application/xml+rss |
| ATOM | application/xml+atom |

* Requires callback query parameter too: ```http://mydomain/api/Customers?callback=foo```

### Designing Results

#### Single Results

Single results should be simple objects
* Member names (naming shouldn't expose server details)
  * just be consistent!
    * camelCasing
    * _underscore

#### Collections

* Wrap the collection around a single object which can contain information about the set.

** Collection Example **

```json
{
	"numberResults": 345,
	"results": [
	{"id": 1,"name": "Pere Pages"},
	{"id": 2,"name": "John Smith"},
	{"id": 3,"name": "Andrew Williams"},
	]
}
```

### ETags (Entit Tags)

* Header to support smart server caching
  * Strong and Weak Caching Support
  * Returned in the Response
* Client should sent ETag back to see if new version is available
  * Request with If-None-Match
  * Use 304 to indicate that it hasn't changed
* Cliend Should Send ETag back to see if new version is available
  * For PUT, use If-Match
  * Use status code if it doesn't match (412 Precondition failed)

** Example **

```
// The ETag shows a version number for the Entity
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Date: Thu, 30 March 2015 08:23:45 GMT
ETag: "4894526782065"
Content-Length: 639
```

```
// Weak ETag, weak cache
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Date: Thu, 30 March 2015 08:23:45 GMT
ETag: W/"4894526782065"
Content-Length: 639
```

** If-None-Match example **

```
// The reponse will have 304 if the entity hasn't changed
GET /api/games/2 HTTP/1.1
Accept: application/json, text/xml
Host: localhost:8863
If-None-Match: "489302392098"
```

** If-Match example **

```
// PUT /api/games/2 HTTP/1.1
// It will retgurn HTTP/1.1 412 Precondition failed if the entity has changed
Accept: application/json, text/xml
Host: localhost: 8863
If-Match: "4893023942098"
```

### Paging

* Lists should always support paging
  * Query String parameters to request paging information
  * Object wrapper to indicate next/prev links
* Can use different page sizes too
  * Limit size of page to limit sever load


** Paging URI example **

```
http://myDomain.com/api/games?page=5&pageSize=50
```

** Paging Result example **

```
{
	"totalREsults": 1958,
	"nextPage" : "http://myDomain/api/games/?page=3",
	"prevPage" : "http://myDomain/api/games/?page=1",
	"results" : [...]
}
```

### Partial Items

* Allow for request of partial items
  * Query String is a common pattern for requesting parts
* Updating of Partial Items
  * Can use PATCH HTTP Verb
  * Update of partial is possible with ETag support

** Update using Patch example **

```
PATCH /api/games/2 HTTP/1.1
Accept: application/json
If-Match: "1234567890"
Host: localhost:8863
Content-Length: 192

{
"id": 2,
"name": "Super Mario Bros",
"price" : 150.0,
"imageUrl" : "...",
...
}
```

** Requesting parts example **

```
http://myDomain.com/api/games/123?fields=id,name,price,imageUrl
```

### Non-Resource APIs

Non resource calls.

* Functional Parts of your API (see example to understand)
  * Be pragmatic and make sure that these parts of our API are documented
  * Be sure that the user can tell it is a different type of operation
  * **Should be completely functional**
  * Don't use them as an excuse to build a PRC API

** Functional Call example **

```
http://myDomain.com/api/calculateTax?state=GA&total=149.99
http://myDomain.com/api/restartServer?isColdBoot=true
http://myDomain.com/api/beginWorldDomination?isVolcanoLairRequired=true
```

## Versioning

## Web Apis Security

## Hypermedia