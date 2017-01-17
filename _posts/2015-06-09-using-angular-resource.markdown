---
layout: post
sidebar-align: left
title: "Using Angular resource"
date: 2015-06-09 19:45:02
categories: javascript angularjs
author: Pere Pages
---

**$resource** service is built on the top of the **$http** service.

|---
| URL | HTTP  | POST | Result
|-|-|-|-|
| http://yourdomain.com/api/books      | GET    | empty | returns all entries    
| http://yourdomain.com/api/books      | POST   | JSON  | creates new entry      
| http://yourdomain.com/api/books/:id  | GET    | empty | returns single entry   
| http://yourdomain.com/api/books/:id  | PUT    | JSON  | updates existing entry 
| http://yourdomain.com/api/books/:id  | DELETE | empty | deletes existing entry 
|---

## How does $resource Work?

"Book" resource example

```javascript
angular.module('myApp.services').factory('Book', function($resource) {
  return $resource('/api/entries/:id'); // Note the full endpoint address
});
```

Methods from the resource

* get() *returns a single entry*
* query() *returns all the entries*
* save() *creates a new an entry*
* remove()
* delete()

```javascript
angular.module('myApp.controllers',[]);
 
angular.module('myApp.controllers').controller('ResourceController',function($scope, Entry) {
  var entry = Entry.get({ id: $scope.id }, function() {
    console.log(entry);
  }); // get() returns a single entry
 
  var entries = Entry.query(function() {
    console.log(entries);
  }); //query() returns all the entries
 
  $scope.entry = new Entry(); //You can instantiate resource class
 
  $scope.entry.data = 'some data';
 
  Entry.save($scope.entry, function() {
    //data saved. do something here.
  }); //saves an entry. Assuming $scope.entry is the Entry object  
});
```

## get()

**/api/books/:id**, :id in the URL is replaced with **$scope.id**.

> It returns an empty object that gets populated when the actual data comes from the server.

The second argument is a callback which is executed when the data arrives from the server.

## query()

**api/books**

> It returns an empty array. This array is populated when the data arrives from the server.

## save()

POST to **/api/entries**

The second argument is a callback which is executed when the data arrives from the server.

## $resource methods

* $save()
* $delete()
* $remove()

```javascript
$scope.book = new Book(); //this object now has a $save() method
$scope.book.$save(function() {
  //data saved. $scope.entry is sent as the post body.
});
```

** $update() **
```javascript
angular.module('myApp.services').factory('Book', function($resource) {
  return $resource('/api/books/:id', { id: '@_id' }, {
    update: {
      method: 'PUT' // this method issues a PUT request
    }
  });
});
```

Setting it to **@_id** means whenever we will call methods like **$update()** and **$delete()** on the resource instance, the value of **:id** will be set to the _id property of the instance. This is useful for **PUT** and **DELETE** requests. Also note the third argument. This is a hash that allows us to add any custom methods to the resource class. If the method issues a non-GET request it's made available to the $resource instance with a **$** prefix.

Assuming we are in the controller

```javascript
$scope.book = Book.get({ id: $scope.id }, function() {
  // $scope.book is fetched from server and is an instance of Book
  $scope.book.data = 'something else';
  $scope.book.$update(function() {
    //updated in the backend
  });
});
```

It does:

1. triggers a PUT request to the URL /api/books/:id
2. reads the value of $scope.book_id and assigns the value to :id and generates the URL
3. sends a PUT request to the URL with $scope.entry as the post body

## $delete()

```javascript
$scope.book = Book.get({ id: $scope.id }, function() {
  // $scope.book is fetched from server and is an instance of Book
  $scope.book.data = 'something else';
  $scope.book.$delete(function() {
    //gone forever!
  });
});
```

It follows the same steps as above, except the request type is DELETE instead of PUT.