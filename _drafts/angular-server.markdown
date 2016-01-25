- Using $resource
- Using $http
- Configuration
- Trnasform & Interceptors

## $resource

The next example does server side logic in the client side, it is **Bad practice**. It is just an example.

Factory and Service

```javascript
app.factory('users', function ($resource) {
	return $resource('/data/users/:id', {id: "@id"});
});

app.value('identity', {});
```

Controller

```javascript 
users.query().$promise.then(function(userCollection) {
	userCollection.forEach(function (user) {
		if(name === user.name && password === user.password) {
			notifier.notify('You have successfully signed in!');
			identity.currentUser = user;
		}
	});
	if(identify.currentUser === undefined) {
		notifier.notify('Username/Password Combination incorrect');
	}
});
``` 

```javascript
// being course a $resource
course.$save();
```

## $http

```javascript
```