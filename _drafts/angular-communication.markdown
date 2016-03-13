## $http


### Solution 2

```javascript
app.factory('followedInstructors', function ($http, $q) {
	return {
		get: function() {
			var dfd = $q.defer();
			$http.get('data/userData/followedInstructors').success(function(data) {
				dfd.resolve(data);
			});
			return dfd.promise;
		},
		save: function() {
			// ...
		}
	};
});
```

### Solution 3

Controller

```javascript
vm.followInstructor = function(instructorName) {
	vm.followedInstructors.push({name: instructorName});
	followedInstructors.save(vm.follwedInstructors);
};
```

Factory

```javascript
app.factory('followedInstructors', function ($http, $q) {
	return {
		get: function() {
			// ...
		},
		save: function(list) {
			$http.post('data/userData/followedInstructors', list);
		}
	};
});
```

## Comparing Promises

### $http promise

Object

- then
- catch
- finally
- success // gives you the data
- error

### $q promise

Object

- then // gives you the data
- catch
- finally

### $resource service

Array

All the data, plus to additional objects $promise and $resolved.

## HTTP Configuration

### Cache

```javascript
$http.get('data/userData/followedInstructors', {cache: true});
```

## Transforms

- transformRequest
- transformResponse

```javascript
$http.post('data/userDAta/followedInstructors', list, {transformRequest: [
	function(data, headersGetter) {
		// manipulate the data
		return data;
}].concat($http.default.transformRequest);
});
```

## Interceptors

Commonly used to add authentication information.

Functions

- request
- requestError
- response
- responseError

```javascript
app.config(function($httpProvider, $provide) {
	$provide.factory('myInterceptor', function() {
		return {
			response: function (config) {
				if(config.config.url === '/data/courses') {
					config.data.splice(5);
				}
				return config;
			}
		};
	});

	$httpProvider.interceptors.push('myInterceptor');
});
```

## Restangular

It's a substitute for $resource.

It has a dependency with *lodash*.


## What is a model for angular?

Objects that represent **data** and **state**.

## Models with $http

## Models with $resource

## Models with Restangular