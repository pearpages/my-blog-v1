# Vanilla Javascript Form Validaton

## Checking If a Form Field is Filled

```html
<form action="" name="form-1">
    <div><label for="">First Name: <input name="first-name" type="text"></label></div>
    <div><label for="">Last Name: <input name="last-name" type="text"></label></div>
</form>
```

```javascript
function validateForm() {
    var x = document.forms["form-1"]["first-name"].value;
    if (x == "") {
        alert("Name must be filled out");
        return false;
    }
}
```

Checking if an input is numeric.

```javascript
// Get the value of the input field with id="numb"
x = document.getElementById("numb").value;

// If x is Not a Number or less than one or greater than 10
if (isNaN(x) || x < 1 || x > 10) {
    text = "Input not valid";
} else {
    text = "Input OK";
}
```

## Browser Required Attribute

> Automatic HTML form validation does not work in Internet Explorer 9 or earlier.

```html
<form action="" method="post">
  <input type="text" name="fname" required> <!-- here -->
  <input type="submit" value="Submit">
</form>
```

## Data validation

* has the user filled in all required fields?
* has the user entered valid date?
* has the unser entered text in a numeric field?

### HTML5 Constraint validation

* HTML Input Attributes
* CSS Pseudo Selectors
* DOM Properties and Methods

#### Constraint Validation HTML Input Attributes

* disabled
* max
* min
* pattern
* required
* type

#### Constraint Validation CSS Pseudo Selectors

* :disabled
* :invalid
* :optional
* :required
* :valid

[CSS presudo classes](http://www.w3schools.com/css/css_pseudo_classes.asp)

#### Constraint Validation API

* checkValidity()
* setCustomValidity()

```javascript
<html>
<head></head>
<body>
<input id="my-number" name="my-number" type="number" min="100" max="300" required>
<button onclick="myFunction()">OK</button>

<p id="demo"></p>

<script>
function myFunction() {
    var inpObj = document.getElementById("my-number");
    if (inpObj.checkValidity() == false) {
        document.getElementById("demo").innerHTML = inpObj.validationMessage;
    }
}
</script>
</body>
</html>
```

#### Constraint Validation DOM Properties

* validity
  + customError
  + patternMismatch
  + rangeOverflow
  + rangeUnderflow
  + stepMismatch
  + tooLong
  + typeMismatch
  + valueMissing
  + valid
* validationMessage
* willValidate

```javascript
<input id="id1" type="number" max="100">
<button onclick="myFunction()">OK</button>

<p id="demo"></p>

<script>
function myFunction() {
    var txt = "";
    if (document.getElementById("id1").validity.rangeOverflow) {
       txt = "Value too large";
    }
    document.getElementById("demo").innerHTML = txt;
}
</script>
```