
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