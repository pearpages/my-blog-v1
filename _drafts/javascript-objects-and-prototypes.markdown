
## Object literal

```javascript
var cat = {name: 'Fluffy', color: 'white'};
console.log(cat);
cat.age = 3;
console.log(cat);
cat.speak = function () {
	console.log("Meeooow");
};
```

## Constructor Functions

```javascript
function Cat(name,color) {
	this.name = name;
	this.color = color;
}

var cat = new Cat('Fluffy','White'); // this is the obect that we create context
// calling new it's like using: Object.create

Cat(); // this is the window or node context
```

## ECMAScript 6 constructor

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