
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