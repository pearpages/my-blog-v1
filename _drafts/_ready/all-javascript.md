# Javascript Basics

## Where To
```javascript
document.getElementById("demo").innerHTML = "Hello JavaScript";
````

```javascript
document.getElementById("demo").style.fontSize = "25px";
````

### Visibility

```javascript
document.getElementById("demo").style.display = "none";
document.getElementById("demo").style.display = "block";
```

### Script Tag

+ header
+ body
+ loading an external file

You can place any number of scripts in an HTML document.

Scripts can be placed in the <body>, or in the <head> section of an HTML page, or in both.

```javascript
<script>
document.getElementById("demo").innerHTML = "My First JavaScript";
</script>
````

Placing scripts at the bottom of the <body> element improves the display speed, because script compilation slows down the display.

```javascript
<!DOCTYPE html>
<html>
<body> 

<h1>A Web Page</h1>
<p id="demo">A Paragraph</p>
<button type="button" onclick="myFunction()">Try it</button>

<script>
function myFunction() {
   document.getElementById("demo").innerHTML = "Paragraph changed.";
}
</script>

</body>
</html>
```

External scripts cannot contain <script> tags.

```javascript
<!DOCTYPE html>
<html>
<body>

<script src="myScript.js"></script>
<script src="/js/myScript1.js"></script>
<script src="http://www.w3schools.com/js/myScript1.js"></script>

</body>
</html>
```

---

## Output
JavaScript can "display" data in different ways:

+ Writing into an HTML element, using innerHTML.
+ Writing into the HTML output using document.write().
+ Writing into an alert box, using window.alert().
+ Writing into the browser console, using console.log().

### innerHTML

```javscsript
document.getElementById("demo").innerHTML = 5 + 6;
```

### document.write()

For testing purposes, it is convenient to use document.write()

> The document.write() method should only be used for testing.

```javascript
<!DOCTYPE html>
<html>
<body>

<h1>My First Web Page</h1>
<p>My first paragraph.</p>

<script>
document.write(5 + 6);
</script>

</body>
</html>
```

Using document.write() after an HTML document is fully loaded, will delete all existing HTML

```javascript
<!DOCTYPE html>
<html>
<body>

<h1>My First Web Page</h1>
<p>My first paragraph.</p>

<button onclick="document.write(5 + 6)">Try it</button>

</body>
</html>
```

### Using window.alert()

```javascript
<!DOCTYPE html>
<html>
<body>

<h1>My First Web Page</h1>
<p>My first paragraph.</p>

<script>
window.alert(5 + 6);
</script>

</body>
</html>
```

### Using console.log()

```javascript
<!DOCTYPE html>
<html>
<body>

<script>
console.log(5 + 6);
</script>

</body>
</html>
```

---

## Syntax
> In HTML, Javascript programs are executed by the web browser.

> Javascript is Case Sensitive.

> JavaScript uses the Unicode character set.

If a JavaScript statement does not fit on one line, the best place to break it, is after an operator.

```javascript
document.getElementById("demo").innerHTML =
"Hello Dolly.";
```

### Keywords

* break
* continue
* debugger
* do ... while
* for
* function
* if ... else
* return
* switch
* try ... catch
* var

### Variables

> It's a good programming practice to declare all variables at the beginning of a script.

```javascript
var person = "John Doe", carName = "Volvo", price = 200;
```

---

## Operators

### Type Operators

* typeof
* instanceof *Returns true if an object is an instance of an object type*

---

## Data Types

* strings
* numbers
* booleans
* arrays
* objects
* null
* undefined
* function

### typeof

```javascript
typeof [1,2,3,4]             // Returns "object" (not "array", see note below)
typeof {name:'John', age:34} // Returns "object"
typeof function myFunc(){}   // Returns "function"
```

### Null

> You can consider it a bug in JavaScript that typeof null is an object. It should be null.

### Difference Between Undefined and Null

```javascript
typeof undefined           // undefined
typeof null                // object
null === undefined         // false
null == undefined          // true
```

---

## Scope
> In JavaScript, scope is the set of variables, objects, and functions you have access to.

> JavaScript has function scope: The scope changes inside functions.

> Do NOT create global variables unless you intend to.

> In "Strict Mode" automatically global variables will fail.

---

## Events

```javascript
<some-HTML-element some-event='some JavaScript'>
```

```javascript
<button onclick="document.getElementById('demo').innerHTML = Date()">The time is?</button>
```

```javascript
<button onclick="displayDate()">The time is?</button>
```

### Common HTML Events

* onchange
* onclich
* onmouseover
* onmouseout
* onkeydown
* onload

[Events Reference](http://www.w3schools.com/jsref/dom_obj_event.asp)

---

## Strings
> All string methods return a new string. They don't modify the original string.
Formally said: **Strings are immutable**: Strings cannot be changed, only replaced.

### String Length

```javascript
var txt = 'Pere Pages';
var sln = txt.length;
```

### Special Characters

```javascript
var x = 'It\'s alright';
var y = "We are the so-called \"Vikings\" from the north."
```

### Find a String in a String

* indexOf *first occurrence*
* search *first occurrence*
* lastIndexOf *last occurrence*

```javascript
var str = "Please locate where 'locate' occurs!";
var pos = str.indexOf("locate");
```

### Extracting String Parts

* slice
* substring *similar to slice, doesn't accept negative values*
* substr *also similar to slice, but the second parameter specificies the **length** of the extracted part*

#### slice()

**slice()** extracts a part of a string and returns the extracted part in a new string.

If a parameter is negative, the position is counted from the end of the string.

If you omit the second parameter, the method will slice out the rest of the string.

```javascript
var str = "Apple, Banana, Kiwi";
var res = str.slice(7,13);
```

### Replacing String Content

The replace() method can also take a regular expression as the search value.

```javascript
str = "Please visit Microsoft!";
var n = str.replace("Microsoft", "W3Schools");
```

### Converting to Upper and Lower Case

```javascript

var text1 = "Hello World!";       // String
var text2 = text1.toUpperCase();  // text2 is text1 converted to upper
```

```javascript
var text1 = "Hello World!";       // String
var text2 = text1.toLowerCase();  // text2 is text1 converted to lower
```

### Concat

The concat() method can be used instead of the plus operator. These two lines do the same.

```javascript
var text = "Hello" + " " + "World!";
var text = "Hello".concat(" ", "World!");
```

### Extracting String Characters

* charAt
* charCodeAt

```javascript
var str = "HELLO WORLD";
str.charAt(0);            // returns H
```

```javascript
 var str = "HELLO WORLD";

str.charCodeAt(0);         // returns 72
```

### Converting a String to An Array

A string can be converted to an array with the split() method.

```javascript
var txt = "a,b,c,d,e";   // String
txt.split(",");          // Split on commas
txt.split(" ");          // Split on spaces
txt.split("|");          // Split on pipe
```

[String Reference](****)

---

## Numbers

> JavaScript has only one type of number.

> JavaScript Numbers are Always 64-bit Floating Point

### Precision

Integers (numbers without a period or exponent notation) are considered accurate up to 15 digits.

```javascript
var x = 999999999999999;   // x will be 999999999999999
var y = 9999999999999999;  // y will be 10000000000000000
```

> The maximum number of decimals is 17, but floating point arithmetic is not always 100% accurate.

### Hexadecimal

```javascript
var x = 0xFF;             // x will be 255
```

### Infinity

```javascript
var myNumber = 2;
while (myNumber != Infinity) {          // Execute until Infinity
    myNumber = myNumber * myNumber;
}
```

```javascript
var x =  2 / 0;          // x will be Infinity
var y = -2 / 0;          // y will be -Infinity
```

```javascript
typeof Infinity;        // returns "number"
```

### NaN *Not aNumber*

```javascript
var x = 100 / "Apple";  // x will be NaN (Not a Number)
```

You can use the global JavaScript function isNaN() to find out if a value is a number.

```javascript
var x = 100 / "Apple";
isNaN(x);               // returns true because x is Not a Number 
```

---

## Number Methods

> All JavaScript data types have a valueOf() and a toString() method.

* toString()
* toExponential()
* toFixed()
* toPrecision()
* valueOf()

### Converting Variables to Numbers

* Number() *object wrapper*
* parseFloat()
* parseInt()

[Number reference](http://www.w3schools.com/jsref/jsref_obj_number.asp)

---

## Math Object

> Unlike other global objects, the Math object has no constructor. Methods and properties are static.



* round()
* pow()
* sqrt()
* abs()
* ceil()
* floor()
* sin()
* cos()
* min()
* max()
* random()

### Constants

```javascript
Math.E        // returns Euler's number
Math.PI       // returns PI
Math.SQRT2    // returns the square root of 2
Math.SQRT1_2  // returns the square root of 1/2
Math.LN2      // returns the natural logarithm of 2
Math.LN10     // returns the natural logarithm of 10
Math.LOG2E    // returns base 2 logarithm of E
Math.LOG10E   // returns base 10 logarithm of E
```


### Random Integers

```javascript
Math.floor(Math.random() * 10);     // returns a number between 0 and 9
Math.floor(Math.random() * 11);      // returns a number between 0 and 10
Math.floor(Math.random() * 100);     // returns a number between 0 and 99
Math.floor(Math.random() * 101);     // returns a number between 0 and 100
Math.floor(Math.random() * 10) + 1;  // returns a number between 1 and 10
Math.floor(Math.random() * 100) + 1; // returns a number between 1 and 100
```

```javascript
function getRndInteger(min, max) {
    return Math.floor(Math.random() * (max - min + 1) ) + min;
}
```

[Math reference](http://www.w3schools.com/jsref/jsref_obj_math.asp)

---

## Javascript Dates

> Dates written as numbers, specifies the number of milliseconds since January 1, 1970, 00:00:00.

### Creating Date objects

```javascript
var d = new Date("October 13, 2014 11:13:00");
var d = new Date(86400000);
var d = new Date(99, 5, 24, 11, 33, 30, 0);
var d = new Date(99, 5, 24);
var d = new Date("2015-03-25");
var d = new Date("2015-03");
```

### Date Formats

> The ISO format follows a strict standard in JavaScript.

> ISO Date	"2015-03-25" (The International Standard)

```javascript
var d = new Date("2015-03-25");
var d = new Date("2015-03-25T12:00:00Z");
```

> UTC (Universal Time Coordinated) is the same as GMT (Greenwich Mean Time).

> Omitting T or Z in a date-time string can give different result in different browser.

---

## Javascript Date Methods

* getDate()	*Get the day as a number (1-31)*
* getDay()	*Get the weekday as a number (0-6)*
* getFullYear()	*Get the four digit year (yyyy)*
* getHours()	*Get the hour (0-23)*
* getMilliseconds()	*Get the milliseconds (0-999)*
* getMinutes()	*Get the minutes (0-59)*
* getMonth()	*Get the month (0-11)*
* getSeconds()	*Get the seconds (0-59)*
* getTime()	*Get the time (milliseconds since January 1, 1970)*

* setDate()	*Set the day as a number (1-31)*
* setFullYear()	*Set the year (optionally month and day)*
* setHours()	*Set the hour (0-23)*
* setMilliseconds()	*Set the milliseconds (0-999)*
* setMinutes()	*Set the minutes (0-59)*
* setMonth()	*Set the month (0-11)*
* setSeconds()	*Set the seconds (0-59)*
* setTime()	*Set the time (milliseconds since January 1, 1970)*

> If adding days, shifts the month or year, the changes are handled automatically by the Date object.

### Compare Dates

```javascript
var today, someday, text;
today = new Date();
someday = new Date();
someday.setFullYear(2100, 0, 14);

if (someday > today) {
    text = "Today is before January 14, 2100.";
} else {
    text = "Today is after January 14, 2100.";
}
document.getElementById("demo").innerHTML = text;
```

[Date Reference](http://www.w3schools.com/jsref/jsref_obj_date.asp)

---

## Javascript Arrays

```javascript
var cars = [
    "Saab",
    "Volvo",
    "BMW"
];

var cars = new Array("Saab", "Volvo", "BMW");

document.getElementById("demo").innerHTML = cars;
```

> JavaScript does not support arrays with named indexes.

> In JavaScript, arrays always use numbered indexes.  

> The new keyword only complicates the code. It can also produce some unexpected results.

### How to Recognize an Array

```javascript
Array.isArray(fruits);     // returns true
```

```javascript
function isArray(x) {
    return x.constructor.toString().indexOf("Array") > -1;
}
```

```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];

fruits instanceof Array     // returns true
```

---

