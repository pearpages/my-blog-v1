# Advanced Console Functionalities

## console.assert

```javascript
var hello = undefined;

if(!hello) {
	console.log('hello not defined');
}

// is the same as

console.assert(hello,'hello not defined');
```

---

## console.count
```javascript
for (var i=0; i < 100; i++) {
	var num = Math.random() * 100;

	if (num > 50) {
		console.count('greater than 50');
	} else {
		console.count('equal below 50');
	}
}
```

---

## console.group / console.groupCollapsed

```javascript
for (var i = 0; i < 100; i++) {
	var num = Math.random() * 100;
	console.groupCollapsed("Group name");
	console.log("car blue");
	console.log("red house");
		console.groupCollapsed("Another nested group");
		console.log(i);
		console.groupEnd();
	console.groupEnd();
}
```

---

## Interpolating values
### Types

+ %s *string*
+ %d *number*
+ %o *object*
+ %c *css*

```javascript
// normal concatenation
console.log("Hello", "world", 123, "foobar");
console.log({foo: "bar", nested: {nested_value: "foobar"}});
// interpolating
console.log("Hello world my name is %s and I am %d years old and here is an object: %o", "Pere Pages", 100, {foo: "foo"});
// css
console.log("whatever output %cipsum","color: red");
```

---

## Console Functions

If we use the different types of console functions we can afterwards use the filters of the browser. To show the ones we want to see.

* warn
* error --> gives *stacktrace* 
* info
* debug

----

## console.time

```javascript
console.time("how long does the for take?");

var array = [];
for (var i = 0; i < 10000000; i++) {
	array.push({index: i});
}

console.timeEnd("how long does the for take?"");
```

---

## console.table

```javascript
function Car(brand, hp) {
	this.brand = brand;
	this.hp = hp;
}

var ferrari = new Car("Ferrari","400cv");
var renault = new Car("Renault","90cv");
var bmw = new Car("BMW","220cv");

var cars = [ferrari,renault,bmw];

var carsByName = {
	ferrari: ferrari,
	renault: renault,
	bmw: bmw
};

console.table(cars);
console.table(carsByName);
console.table(cars,["brand"]);
```

#blog #console