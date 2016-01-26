
## Objects

### Object literal

```javascript
var cat = {name: 'Fluffy', color: 'white'};
console.log(cat);
cat.age = 3;
console.log(cat);
cat.speak = function () {
	console.log("Meeooow");
};
```

### Constructor Functions

```javascript
function Cat(name,color) {
	this.name = name;
	this.color = color;
}

var cat = new Cat('Fluffy','White'); // this is the obect that we create context
// calling new it's like using: Object.create

Cat(); // this is the window or node context
```

### ECMAScript 6 constructor

```javascript
class Cat {
	constructor(name,color) {
		this.name = name;
		this.color = color;
	}

	speak() {
		console.log('Meeeooow');
	}
}

var cat = new Cat('Fluffy','White');
cat.speak();
```

## Object Properties

- value
- writable
- enumerable
- configurable

### Accessing

```javascript
var car = {doors:4, color: 'blue'};

console.log(car.doors);
console.log(car['doors']);
```

### Writable

```javascript
Object.defineProperty(cat, 'name', {writable:false});

cat.name = 'John'; // does not change the name property
```

But it the property 'points' to an object, this object can still change. Then we need to do:

```javascript
var cat = {
	name:'Fluffy',
	color: 'White',
	attributes: {attr1: 'abc', attr2: 'abc'}
}
Object.freeze(cat.attributes);
```

### Enumerable

```javascript
Object.keys(cat);
```

We can use ```// for... in``` to loop through object properties.

```javascript
for (var popertyName in cat) {
	console.log(cat[propertyName]);
}
```

```javascript
Object.defineProperty(cat, 'name', {enumerable:false});
Object.keys(cat); // name shouldn't be part of it

// it is not enumerable it doesn't show in stringify either
JSON.stringify(cat); // stringify ignores functions
```` 

### Configurable

Once we change the property configurable to false it is impossible to put it to true back again.

```javascript
Object.defineProperty(car, 'doors', {configurable: false});
Object.defineProperty(car, 'doors', {configurable: true}); // this does not work because of the prior sentence
delete(car.doors); // won't work either
```

### Getters and Setters

```javascript
Object.defineProperty(cat, 'fullName',
	{
		get: function() {
			return this.name.first + ' ' + this.name.last
		},
		set: function(value) {
			var nameParts = value.split(' ');
			this.name.first = nameParts[0];
			this.name.last = nameParts[1];
		}
	}
});

cat.fullName = 'Muffin Top';
console.log(cat.fullName);
console.log(cat.name.first);
console.log(cat.name.last);
```

## JavaScript Prototypes and Inheritance

```javascript
'use strict';

var arr = ['red','blue','green'];

Object.defineProperty(arr, 'last', {get: function() {
	return this[this.length-1];
}});

var last = arr.last;

var arr2 = ['one','two','three'];
display(arr2.last); // undefined
```

But if we use

```javascript
'use strict';

var arr = ['red','blue','green'];

Object.defineProperty(Array.prototype, 'last', {get: function() { // Array.prototype
	return this[this.length-1];
}});

var last = arr.last; // gets last

var arr2 = ['one','two','three'];
console.log(arr2.last); // shows last
```

### Prototype

Functions have **prototype**.

Objects have **__proto__**.

#### Function's prototype

A function's prototype is the object **instance** that will become the prototype for all obects created using this function as a constructor.

#### Object's prototype

An object's prototype is the object **instance** from which the object is inherited.

#### Examples

```javascript
function Cat(name,color) {
	this.name = name;
	this.color = color;
}

var fluffy = new Cat('Fluffy','White');

console.log(Cat.prototype); // empty
console.log(fluffy.__proto__) // empty, is the same as the above
console.log(Cat.prototype === fluffy.__proto__) // true

Cat.prototype.age = 3;

display(cat.prototype);
display(fluffy.__proto__); / both also display the same


```


