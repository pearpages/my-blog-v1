# Javascript HTML

> DOM: Document Object Model

* Core DOM - standard model for all document types
* XML DOM - standard model for XML documents
* HTML DOM - standard model for HTML documents

> The HTML DOM is a standard for how to get, change, add, or delete HTML elements.

JavaScript can :

* change / remove / add elements in the page
* change / remove / add attributes in the page
* change all CSS styles in the page
* react and create events in the page

---

## Methods

In the DOM, all HTML elements are defined as **objects**.

A **property** is a value that you can get or set (like changing the content of an HTML element).

A **method** is an action you can do (like add or deleting an HTML element).

```javascript
<html>
<body>

<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = "Hello World!";
// getElementById is a 'method'
// innerHTML is a 'property'
</script>

</body>
</html>
```

* getElementById
* innerHTML

> The innerHTML property can be used to get or change any HTML element, including <html> and <body>.

---

## Document

### Finding Elements

* document.getElementById(id)
* document.getElementsByTagName(name)
* document.getElementsByClassName(name)

### Changing HTML Elements

* element.innerHTML = html
* element.attribute = value
* element.setAttribute(attribute,value)
* element.stye.property = style

### Adding and Deleting Elements

* document.createElement(element)	
* document.removeChild(element)	
* document.appendChild(element)	
* document.replaceChild(element)	
* document.write(text)	

### Adding Events Handlers

* document.getElementById(id).onclick = function(){code}

### Finding HTML objects

document.anchors	<a>
document.baseURI	Returns the absolute base URI of the document	3
document.body	<body>
document.cookie	
document.documentElement	<html>
document.documentURI	
document.domain	
document.embeds	<embed>
document.forms	<form>
document.head	<head>
document.images	<img>
document.links	all <area> and <a> elements that have a href
document.readyState	Returns the (loading) status of the document
document.referrer	Returns the URI of the referrer (the linking document)
document.scripts	<script>
document.title	<title>
document.URL

---

## Elements

```javascript
var myElement = document.getElementById("intro");

var allP = document.getElementsByTagName("p");

var allIntroClasses = document.getElementsByClassName("intro");
```

This example finds the element with id="main", and then finds all <p> elements inside "main":

```javascript
var x = document.getElementById("main");
var y = x.getElementsByTagName("p");
```

### By Query Selector

```javascript
// also querySelector
var x = document.querySelectorAll("p.intro");
```

---

## HTML

> Never use document.write() after the document is loaded. It will overwrite the document.

* innerHTML
* attribute

```javascript
document.getElementById("myImage").src = "landscape.jpg";
```

---

## CSS

```javascript
document.getElementById("p2").style.color = "blue";
```

```javascript
<h1 id="id1">My Heading 1</h1>

<button type="button" 
onclick="document.getElementById('id1').style.color = 'red'">
Click Me!</button>
```

```javascript
<p id="p1">
This is a text.
This is a text.
This is a text.
This is a text.
</p>

<input type="button" value="Hide text" onclick="document.getElementById('p1').style.visibility='hidden'">
<input type="button" value="Show text" onclick="document.getElementById('p1').style.visibility='visible'">
```

---

## Animations

```javascript
<!DOCTYPE html>
<html>
<style>
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: yellow;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background-color: red;
}
</style>
<body>

<p>
<button onclick="myMove()">Click Me</button>
</p> 

<div id ="container">
<div id ="animate"></div>
</div>

<script>
function myMove() {
  var elem = document.getElementById("animate");   
  var pos = 0;
  var id = setInterval(frame, 5);
  function frame() {
    if (pos == 350) {
      clearInterval(id);
    } else {
      pos++; 
      elem.style.top = pos + 'px'; 
      elem.style.left = pos + 'px'; 
    }
  }
}
</script>

</body>
</html>
```

---

## Events

```javascript
<!DOCTYPE html>
<html>
<body>

<h1 onclick="this.innerHTML = 'Ooops!'">Click on this text!</h1>

</body>
</html>
```

```javascript
<!DOCTYPE html>
<html>
<body>

<h1 onclick="changeText(this)">Click on this text!</h1>

<script>
function changeText(id) { 
    id.innerHTML = "Ooops!";
}
</script>

</body>
</html>
```

### Event attributes

e.g. 

* onclick
* onload
* onchange
* onmouseover
* onmouseout
* onmousedown
* onmouseup
* onfocus

```html
<button onclick="displayDate()">The time is?</button>
```

### Assign Events Using the HTML DOM

```javascript
document.getElementById("myBtn").onclick = displayDate;
```

### The onload and onunload Events

The onload and onunload events are triggered when the user **enters or leaves the page**.

The onload event can be used to check the visitor's browser type and browser version, and load the proper version of the web page based on the information.

The onload and onunload events can be used to deal with **cookies**.

```html
<body onload="checkCookies()">
```

```html
<!DOCTYPE html>
<html>
<body onload="checkCookies()">

<p id="demo"></p>

<script>
function checkCookies() {
    var text = "";
    if (navigator.cookieEnabled == true) {
        text = "Cookies are enabled.";
    } else {
        text = "Cookies are not enabled.";
    }
    document.getElementById("demo").innerHTML = text;
}
</script>

</body>
</html> 
```

### The onchange Event

```html
<input type="text" id="fname" onchange="upperCase()">
```

### The onmouseover and onmouseout Events

```html
<!DOCTYPE html>
<html>
<body>

<div onmouseover="mOver(this)" onmouseout="mOut(this)" 
style="background-color:#D94A38;width:120px;height:20px;padding:40px;">
Mouse Over Me</div>

<script>
function mOver(obj) {
    obj.innerHTML = "Thank You"
}

function mOut(obj) {
    obj.innerHTML = "Mouse Over Me"
}
</script>

</body>
</html> 
```

### The onmousedown, onmouseup and onclick Events

```html
<!DOCTYPE html>
<html>
<body>

<div onmousedown="mDown(this)" onmouseup="mUp(this)"
style="background-color:#D94A38;width:90px;height:20px;padding:40px;">
Click Me</div>

<script>
function mDown(obj) {
    obj.style.backgroundColor = "#1ec5e5";
    obj.innerHTML = "Release Me";
}

function mUp(obj) {
    obj.style.backgroundColor="#D94A38";
    obj.innerHTML="Thank You";
}
</script>

</body>
</html> 
```

[HTML DOM Event Object Reference](http://www.w3schools.com/jsref/dom_obj_event.asp)

---

## EventListener

You can add many event handlers to one element.

You can easily remove an event listener by using the removeEventListener() method.

### addEventListener() method

```javascript
document.getElementById("myBtn").addEventListener("click", displayDate);
```

The third parameter is a boolean value specifying whether to use event bubbling or event capturing. This parameter is optional.

```
element.addEventListener(event, function, useCapture);
```

```javascript
element.addEventListener("click", function(){ alert("Hello World!"); });
```

```javascript
element.addEventListener("click", myFunction);

function myFunction() {
    alert ("Hello World!");
}
```

### Add Many Event Handlers to the Same Element

```javascript
element.addEventListener("click", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);
```

### Add an Event Handler to the Window Object

The addEventListener() method allows you to add event listeners on any HTML DOM object such as HTML elements, the HTML document, the window object, or other objects that support events, like the xmlHttpRequest object.

```javascript
window.addEventListener("resize", function(){
    document.getElementById("demo").innerHTML = sometext;
});
```

### Passing Parameters

```html
<!DOCTYPE html>
<html>
<body>

<p>This example demonstrates how to pass parameter values when using the 
addEventListener() method.</p>

<p>Click the button to perform a calculation.</p>

<button id="myBtn">Try it</button>

<p id="demo"></p>

<script>
var p1 = 5;
var p2 = 7;

document.getElementById("myBtn").addEventListener("click", function() {
    myFunction(p1, p2);
});

function myFunction(a, b) {
    var result = a * b;
    document.getElementById("demo").innerHTML = result;
}
</script>

</body>
</html>
```

### Event Bubbling or Event capturing

#### Bubbling

In *bubbling* the inner most element's event is handled first and then the outer: the <p> element's click event is handled first, then the <div> element's click event.

#### Capturing

In *capturing* the outer most element's event is handled first and then the inner: the <div> element's click event will be handled first, then the <p> element's click event.

```
// With the addEventListener() method you can specify the propagation type by using the "useCapture" parameter
addEventListener(event, function, useCapture);
```

> The default value is false, which will use the bubbling propagation, when the value is set to true, the event uses the capturing propagation.

```javascript
document.getElementById("myP").addEventListener("click", myFunction, true);
document.getElementById("myDiv").addEventListener("click", myFunction, true);
```

### removeEventListner()

```javascript
element.removeEventListener("mousemove", myFunction);
```

[HTML DOM Event Object Reference](http://www.w3schools.com/jsref/dom_obj_event.asp)

---

## Navigation

### DOM Nodes

> According to the W3C HTML DOM standard, everything in an HTML document is a node

* entire document
* every HTML element
* text inside HTML elements
* every HTML attribute
* all comments

With the HTML DOM, all nodes in the node tree can be accessed by JavaScript.

New nodes can be created, and all nodes can be modified or deleted.

### Node Relationships

* root
* parent (only one)
* children
* siblings

### Navigating Between Nodes

* parentNode
* childNodes[nodenumber]
* firstChild
* lastChild
* nextSibling
* previousSibling

> A common error in DOM processing is to expect an element node to contain text.

```html
<title id="demo">DOM Tutorial</title>
```

The element node <title> (in the example above) does not contain text.

It contains a **text node** with the value "DOM Tutorial".

```javascript
// The value of the text node can be accessed by the node's innerHTML property.
var myTitle = document.getElementById("demo").innerHTML;

// Accessing the innerHTML property is the same as accessing the **nodeValue** of the first child:

var myTitle = document.getElementById("demo").firstChild.nodeValue;

// or

var myTitle = document.getElementById("demo").childNodes[0].nodeValue;
```

### DOM Root Nodes

* document.body (the body)
* document.documentElement (the full document)

### The nodeName property

* is read-only
* **tag** name for an element node
* of a text node is **#text**
* the document node is always **#document**

### The nodeValue property

* elment nodes is **undefined**
* text nodes is the text
* of attributes is the attribute

### nodeType property

* Element
* Attribute
* Text
* Comment
* Document

---

## Nodes

### Creating New HTML Elements (Nodes)

To add a new element to the HTML DOM, you must create the element (element node) first, and then append it to an existing element.

```javascript
var para = document.createElement("p");
var node = document.createTextNode("This is new.");
para.appendChild(node);

var element = document.getElementById("div1");
element.appendChild(para);
```

### insertBefore()

```javascript
var para = document.createElement("p");
var node = document.createTextNode("This is new.");
para.appendChild(node);

var element = document.getElementById("div1");
var child = document.getElementById("p1");
element.insertBefore(para,child);
```

### Removing Existing HTML Elements

> It would be nice to be able to remove an element without referring to the parent.
But sorry. The DOM needs to know both the element you want to remove, and its parent.

```javascript
var parent = document.getElementById("div1");
var child = document.getElementById("p1");
parent.removeChild(child);
```

**Use it that way**

```javascript
var child = document.getElementById("p1");
child.parentNode.removeChild(child);
```

### Replacing HTML Elements

To replace an element to the HTML DOM, use the replaceChild() method.

```javascript
var para = document.createElement("p");
var node = document.createTextNode("This is new.");
para.appendChild(node);

var parent = document.getElementById("div1");
var child = document.getElementById("p1");
parent.replaceChild(para, child);
```

---

## Nodelist

```javascript
var x = document.getElementsByTagName("p");

// The nodes can be accessed by an index number. To access the second <p> node you can write:

y = x[1];
```

### List Length

```javascript
var myNodelist = document.getElementsByTagName("p");
document.getElementById("demo").innerHTML = myNodelist.length;
```

> *A node list is not an array!* 
A node list may look like an array, but it is not. You can loop through the node list and refer to its nodes like an array. However, you cannot use Array Methods, like valueOf() or join() on the node list.

```javascript
var myNodelist = document.getElementsByTagName("p");
var i;
for (i = 0; i < myNodelist.length; i++) {
    myNodelist[i].style.backgroundColor = "red";
}
```

---