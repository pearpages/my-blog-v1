# javascript-arrays

## Basic

```javascript
var data = [
    {symbol: "ABC", price: 140.22, volume: 54432 },
    {symbol: "RTY", price: 532.19, volume: 134 },
    {symbol: "FGH", price: 340.22, volume: 4323 }
];

// forEach
function getStocksSymbolsWithForEach(stocks) {
    var res = [];

    stocks.forEach(function (stock) {
        res.push(stock.symbol);
    });

    return res;
} 

// map
function getStocksSymbolsWithMap(stocks) {
    return stocks.map(function (stock) {
        return stock.symbol;
    });
}

// filter
function getStocksOver(stocks,minPrice) {
    return stocks.filter(function (stock) {
        return stock.price >= minPrice;
    });
}

// filter and map combined
function getFilteredStockSymbols(stocks) {
    stocks
        .filter(function(stock) {
            return stock.price >= 150.00;
        })
        .map(function(stock) {
            return stock.symbol;
        });
}
```

---

## Function Examples

See */examples/main.js* if you want to run the examples.

* concat
* joinSplitCharAt
* indexOf
* slice
* sort
* filter
* some
* push
* every

### concat

```javascript
// Concat 
// It retuns a new array !!!
// The new array is the merge of the selected plus the ones you want to concatenate

// IMPORTANT
// Object references (and not the actual object): concat copies object references into the new array. 
// Both the original and new array refer to the same object. 
// That is, if a referenced object is modified, the changes are visible to both the new and original arrays.

var items = [1, 2];
var newItems = items.concat(3, 4, 5, 6);

console.log(newItems);

// It can flatten arrays but only one level

var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];
var arr3 = [7, 8, 9];

var merge = arr1.concat(arr2, arr3);
console.log(merge);

// An example:

var people = [
    { name: 'Shane' },
    { name: 'Sally' }
];
var people2 = [{ name: 'Simon' }, { name: 'Ben' }];

people.concat(people2).forEach((v) => console.log(v.name));
```

---

### joinSplitCharAt

```javascript
// Join

var names = ['Shane', 'Alan', 'Osbourne'];
console.log(names.join(' '));

var html = [];
html.push('<div>');
html.push('<p>Hello World!</p>');
html.push('</div>');

console.log(html.join(''));

// another example

var name = 'shane osbourne';

var res = name.split(' ')
    .map((e) => e.charAt(0).toUpperCase() + e.slice(1))
    .join(' ');

console.log(res);
```

---

### indexOf

```javascript
// with strings

var family1 = ['Shane', 'Sally', 'Isaac', 'Kittie'];

function exists(group, value) {
    return (group.indexOf(value) !== -1);
}

console.log(exists(family1, 'Kittie'));
console.log(exists(family1, 'John'));

// with objects

var shane = {
    name: 'Shane'
}
var sally = {
    name: 'Sally'
}
var kittie = {
    name: 'Kittie'
}

var family2 = [shane, sally];

console.log(exists(family2, shane));
console.log(exists(family2, kittie));

// case example, filtering files

var whitelist = ['.css', '.js'];
var events = [
    {
        file: 'css/core.css'
    },
    {
        file: 'js/app.js'
    },
    {
        file: 'index.html'
    }
];

var filtered = events.filter((event) => {
    var ext = require('path').extname(event.file);
    return exists(whitelist, ext);
});
console.log(filtered);
```

---

### slice

```javascript
// slice lets us copy an array
// BUT it doesn't work well with objects, because it only copies the reference

var items = [1, 2, 3, 4, 5];
var copy = items.slice();

copy.push(6);

console.log(items, copy);

// for slicing you have to indicate the first and the last index, but the last index is not included

var items2 = [1, 2, 3, 4, 5];
console.log(items.slice(2)); // [3,4,5]
console.log(items.slice(2, 4)); // [3,4]
console.log(items.slice(2, 5)); // [3,4,5]
console.log(items.slice(-1)); // [5]
console.log(items.slice(-3)); // [3,4,5]
```

---

### sort

```javascript
// RETURNS the same array modified!

// it's useful for sorting strings, and strings only

var items = ['john', 'John', 'Mary', 'Paul']; // ['John','Mary','Paul','john']
console.log(items.sort());

// sorting numbers

var numbers = [134, 4545, 345, 98];
console.log(numbers.sort((a, b) => a - b)); // ascending
console.log(numbers.sort((a, b) => b - a)); // descending

// example

var lessons = [
    {
        title: 'lesson1',
        views: 1000
    },
    {
        title: 'lesson2',
        views: 1050
    },
    {
        title: 'lesson3',
        views: 1025
    }
];

var list = lessons
    .sort((a, b) => b.views - a.views) // descending
    .map(x => `  <li>${x.title} (${x.views})</li>`)
    .join('\n');

var output = `<ul>\n${list}\n</ul>`;
console.log(output);
```

---

### filter

```javascript
// creates a new array!
// the new array will content only the elements that return true

var items = [1, 2, 3, 4, 5];

console.log(items.filter(x => x > 3));
```

---

### some

```javascript
// check if there's at least one element in the array with the property asked

var elements = ['car', 'house', 'key', 'ball'];
console.log(elements.some((x) => x === 'key')); // true
console.log(elements.some((x) => x === 'plane')); // false
```

---

### push

```javascript
// push modifies the current array but concat creates a new array
// it retuns the lenght of the array

var elements = [];
elements.push(1);
elements.push(2);
elements.push(3);
console.log(elements); // [1,2,3];
elements.push(4, 5, 6);
console.log(elements); // [1,2,3,4,5,6];

elements2 = [1, 2, 3, 4, 5, 6];
elements.push.apply(elements, elements2);
console.log(elements);
```

---

### every

```javascript
// checks that all the elements have the same property
```

---

## Using Observables

### Old Way

```javascript
var button = document.createElement("BUTTON");        // Create a <button> element
var text = document.createTextNode("CLICK ME");       // Create a text node
button.appendChild(text);                                // Append the text to <button>
document.body.appendChild(button);    

var handler = function(e) {
    alert('clicked');
    button.removeEventListener('click',handler);
};

button.addEventListener('click',handler); // so the event handler only works once
```

### Using Observables

```javascript
var button = document.createElement("BUTTON");        // Create a <button> element
var text = document.createTextNode("CLICK ME");       // Create a text node
button.appendChild(text);                                // Append the text to <button>
document.body.appendChild(button);    

var filename = 'https://cdnjs.cloudflare.com/ajax/libs/rxjs/5.0.1/Rx.js';

var fileref = document.createElement('script');
fileref.setAttribute("type","text/javascript");
fileref.setAttribute("src", filename);
fileref.onload = onLoad;
document.getElementsByTagName("head")[0].appendChild(fileref);

function onLoad() {
    var clicks = Rx.Observable.fromEvent(button,'click');

    clicks.subscribe( function (res) {
            alert('clicked');   
        }
    );
}

```

```javascript
// load a js file dynamically
var js = document.createElement("script");
js.type = "text/javascript";
js.src = filename;
js.onload = onLoad;
document.body.appendChild(js);
```

### Map Method in Observables

```javascript
var button = document.createElement("BUTTON");        // Create a <button> element
var text = document.createTextNode("CLICK ME");       // Create a text node
button.appendChild(text);                                // Append the text to <button>
document.body.appendChild(button);    

var filename = 'https://cdnjs.cloudflare.com/ajax/libs/rxjs/5.0.1/Rx.js';

var fileref = document.createElement('script');
fileref.setAttribute("type","text/javascript");
fileref.setAttribute("src", filename);
fileref.onload = onLoad;
document.getElementsByTagName("head")[0].appendChild(fileref);

function onLoad() {
    var clicks = Rx.Observable.fromEvent(button,'click')
        .map(function (e) {
            return {x: e.clientX, y: e.clientY};
        });

    clicks.subscribe( function (res) {
            console.log(res);
        }
    );
}
```