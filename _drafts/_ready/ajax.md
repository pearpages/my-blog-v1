# AJAX
```javascript
variable = new XMLHttpRequest();
```

---
## XMLHttp
### Methods

+ new XMLHttpRequest()
+ abort() *cancels the current request*
+ getAllResponseHeaders() *returns header information*
+ getResponseHeader() *returns specific header information*
+ open(method,url,async,user,psw)
+ send() *for GET*
+ send(string) *for POST*
+ setRequestHeader() *Adds a label/value pair to the header to be sent*

### Properties

+ onreadystatechange *Defines a function to be called when the readyState property changes*
+ readyState
+ responseText
+ responseXML
+ status *200,403,404*
+ statusText

### readyState

+ 0: request not initizialez
+ 1: server connection established
+ 2: request received
+ 3: processing request
+ 4: request finished and response is ready

## Example
```html
<!DOCTYPE html>
<html>
<body>

<h1>The XMLHttpRequest Object</h1>

<p id="demo">Let AJAX change this text.</p>

<button type="button" onclick="loadDoc()">Change Content</button>

<script>
function loadDoc() {
  var xhttp;
  if (window.XMLHttpRequest) {
    // code for modern browsers
    xhttp = new XMLHttpRequest();
    } else {
    // code for IE6, IE5
    xhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "ajax_info.txt", true);
  xhttp.send();
}
</script>

</body>
</html>
```

---

## Request

### GET

```javascript
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```

### Non-Cache GET

```javascript
xhttp.open("GET", "demo_get2.asp?fname=Henry&lname=Ford", true);
xhttp.send();
```

### POST

```javascript
xhttp.open("POST", "demo_post.asp", true);
xhttp.send();
```

```javascript
xhttp.open("POST", "ajax_test.asp", true);
xhttp.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
xhttp.send("fname=Henry&lname=Ford");
```

### Non Asynchronously

```javascript
xhttp.open("GET", "ajax_info.txt", false);
xhttp.send();
document.getElementById("demo").innerHTML = xhttp.responseText;
```
----
## Response

> The **readyState** property holds the status of the XMLHttpRequest.

> The **onreadystatechange** property defines a function to be executed when the readyState changes.

> The **status** property and the **statusText** property holds the status of the XMLHttpRequest object.


```javascript
function loadDoc() {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            document.getElementById("demo").innerHTML =
            this.responseText;
       }
    };
    xhttp.open("GET", "ajax_info.txt", true);
    xhttp.send(); 
}
```

```javascript
loadDoc("url-1", myFunction1);

loadDoc("url-2", myFunction2);

function loadDoc(url, cFunction) {
  var xhttp;
  xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      cFunction(this);
    }
  };
  xhttp.open("GET", url, true);
  xhttp.send();
}

function myFunction1(xhttp) {
  // action goes here
} 
function myFunction2(xhttp) {
  // action goes here
}
```

### The getAllResponseHeaders() Method

The getAllResponseHeaders() method returns all header information from the server response.

```javascript
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    document.getElementById("demo").innerHTML =
    this.getAllResponseHeaders();
  }
};
```

### The getResponseHeader() Method

```javascript
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    document.getElementById("demo").innerHTML =
    this.getResponseHeader("Last-Modified");
  }
};
xhttp.open("GET", "ajax_info.txt", true);
xhttp.send();
```
---

#javascript