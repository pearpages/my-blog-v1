---
layout: post
sidebar-align: left
title:  "REST Services (REpresentational State Transfer)"
date:   2015-05-14 15:00:25
categories: web javascript json
---

Clients can be developed independently of the REST services using mock data. REST services can likewise be developed independently of the client.

REST services should be **stateless**. A REST service **should never hold data in a session variable**. All information needed for a REST service call should be contained in the request and header passed from the client to the service. Any state should be held in the client and not in the service.

## Constrants

* It's URL-based
* It uses and Internet media type such as JSON for data interchange.
* It uses standard methods (GET,PUT,POST,DELETE).

## HTTP Methods

* POST
    - Create new resources.
    - Retrieve a list of resources when a large amount of request data is required to be passed to the service.
* PUT
    - Update a resource.
* GET 
    - Retrieve a resource or list of resources.
* DELETE
    - Delete a resource.


