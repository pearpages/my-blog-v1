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

### Solution 1

```javascript
app.factory('followedInstructors', function ($http) {
	return {
		get: function() {
			return $http.get('data/userData/followedInstructors');
		},
		save: function() {
			// ...
		}
	};
});
```

Controller

```javascript
followedInstructors.get().success(function(data) {});
```

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

