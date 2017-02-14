# CSS

## Background

+ background	*Sets all the background properties in one declaration*
+ background-attachment	*Sets whether a background image is fixed or scrolls with the rest of the page*
+ background-color	*Sets the background color of an element*
+ background-image	*Sets the background image for an element*
+ background-position	*Sets the starting position of a background image*
+ background-repeat	*Sets how a background image will be repeated*

```css
body {
    background-image: url("gradient_bg.png");
    background-repeat: repeat-x;
}
```

```css
body {
    background-image: url("img_tree.png");
    background-repeat: no-repeat;
}
```

### background-attachment

> To specify that the background image should be fixed (will not scroll with the rest of the page).

```css
body {
    background-image: url("img_tree.png");
    background-repeat: no-repeat;
    background-position: right top;
    background-attachment: fixed;
}
```

---

## Borders

+ border	*Sets all the border properties in one declaration*
+ border-color	*Sets the color of the four borders*
+ border-radius	*Sets all the four border-*-radius properties for rounded corners*
+ border-style	*Sets the style of the four borders*
+ border-top	*Sets all the top border properties in one declaration*
+ border-width	*Sets the width of the four borders*

```css
p.mix {border-style: dotted dashed solid double;}
```

---

## Height / width

+ height	*Sets the height of an element*
+ max-height	*Sets the maximum height of an element*
+ max-width	*Sets the maximum width of an element*
+ min-height	*Sets the minimum height of an element*
+ min-width	*Sets the minimum width of an element*
+ width	*Sets the width of an element*

---

## Box Model

+ Content  *The content of the box, where text and images appear*
+ Padding  *Clears an area around the content. The padding is transparent*
+ Border  *A border that goes around the padding and content*
+ Margin  *Clears an area outside the border. The margin is transparent*

```css
div {
    width: 320px;
    padding: 10px;
    border: 5px solid gray;
    margin: 0; 
}
```

> Total element width = width + left padding + right padding + left border + right border + left margin + right margin

---

## Outline

> However, the outline property is different from the border property - The outline is NOT a part of an element's dimensions; the element's total width and height is not affected by the width of the outline.

+ outline	 *Sets all the outline properties in one declaration*
+ outline-color	 *Sets the color of an outline*
+ outline-offset	 *Specifies the space between an outline and the edge or border of an element*
+ outline-style	 *Sets the style of an outline*
+ outline-width	 *Sets the width of an outline*

---

## Text

+ color	 *Sets the color of text*
+ direction	 *Specifies the text direction/writing direction*
+ letter-spacing	 *Increases or decreases the space between characters in a text*
+ line-height	 *Sets the line height*
+ text-align	 *Specifies the horizontal alignment of text*
+ text-decoration	 *Specifies the decoration added to text*
+ text-indent	 *Specifies the indentation of the first line in a text-block*
+ text-shadow	 *Specifies the shadow effect added to text*
+ text-transform	 *Controls the capitalization of text*
+ text-overflow	 *Specifies how overflowed content that is not displayed should be signaled to the user*
+ unicode-bidi	 *Used together with the direction property to set or return whether the text should be overridden to support multiple languages in the same document*
+ vertical-align	 *Sets the vertical alignment of an element*
+ white-space	 *Specifies how white-space inside an element is handled*
+ word-spacing	 *Increases or decreases the space between words in a text*

---

## Fonts

* Serif
* Sans-Serif
* Monospace

+ font	 *Sets all the font properties in one declaration*
+ font-family	 *Specifies the font family for text*
+ font-size	 *Specifies the font size of text*
+ font-style	 *Specifies the font style for text*
+ font-variant	 *Specifies whether or not a text should be displayed in a small-caps font*
+ font-weight	 *Specifies the weight of a font*

---

## Icons

+ Font Awesome Icons
+ Bootstrap Icons
+ Google Icons

---

## Links

* a:link - a normal, unvisited link
* a:visited - a link the user has visited
* a:hover - a link when the user mouses over it
* a:active - a link the moment it is clicked

---

## Lists

* list-style-type (if a list-style-image is specified, the value of this property will be displayed if the image for some reason cannot be displayed)
* list-style-position (specifies whether the list-item markers should appear inside or outside the content flow)
* list-style-image (specifies an image as the list item marker)

---

## Position

* bottom	
* clip	*Clips an absolutely positioned element*
* cursor	*Specifies the type of cursor to be displayed*
* left	
* overflow	
* overflow-x
* overflow-y
* position	
* right	
* top	
* z-index	

---

## Overflow

+ visible
+ hidden
+ scroll
+ auto

* overflow	
* overflow-x
* overflow-y

---

## Float

### clearfix Hack

```css
.clearfix {
    overflow: auto;
}
```

```css
.clearfix::after {
    content: "";
    clear: both;
    display: table;
}
```

+ clear
+ float
+ overflow
+ overflow-x
+ overflow-y

---

## Align

### Center Align elements

```css
.center {
    margin: auto; /* <-- the key */
    width: 50%;
}
```

### Center Align Text

```css
.text {
    text-align: center;
}

```

### Center image

```css
img {
    display: block;
    margin: auto;
    width: 40%;
}
```

### Left and Right Align - Using position

```css
.right {
    position: absolute;
    right: 0px;
    width: 300px;
}
```

### Let and Right Align - Using float

```css
.right {
    float: right;
    width: 300px;
}
```

> Tip: When aligning elements with float, always define margin and padding for the <body> element. This is to avoid visual differences in different browsers.

### Center Vertically - Using padding

```css
.center {
    padding: 70px 0;
}
```

```css
.center {
    padding: 70px 0;
    text-align: center;
}
```

### Center Vertically - Using line-height

> Another trick is to use the **line-height** property with a value that is equal to the **height** property.

```css
.center {
    line-height: 200px;
    height: 200px;
    text-align: center;
}

/* If the text has multiple lines, add the following: */
.center p {
    line-height: 1.5;
    display: inline-block;
    vertical-align: middle;
}
```

### Center Vertically - Using position & transform

```css
.center { 
    height: 200px;
    position: relative;
    border: 3px solid green; 
}

.center p {
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

---

## Combinators

> A combinator is something that explains the relationship between the selectors.

+ descendant selector (space)
+ child selector (>) *that are the immediate children of a specified element*
+ adjacent sibling selector (+) *same parent, immediately after*
+ general sibling selector (~) *same parent, all siblings*

---

## Pseudo-classes

> A pseudo-class is used to define a special state of an element.

.e.g.

+ :hover
+ :link /* unvisited link */
+ :visited
+ :active
+ :hover
+ :first-child


```
selector:pseudo-class {
    property:value;
}
```

### Right order

1. :link,:visited
2. :hover
3. :active

### :lang

```html
<html>
<head>
<style>
q:lang(no) {
    quotes: "~" "~";
}
</style>
</head>

<body>
<p>Some text <q lang="no">A quote in a paragraph</q> Some text.</p>
</body>
</html>
```

### all

+ :active	
+ :checked
+ :disabled	
+ :empty	
+ :enabled
+ :first-child	
+ :first-of-type	
+ :focus
+ :hover	
+ :in-range	
+ :invalid	
+ :lang(language)	
+ :last-child	
+ :last-of-type	
+ :link	
+ :not(selector)	
+ :nth-child(n)	
+ :nth-last-child(n)
+ :nth-last-of-type(n)
+ :nth-of-type(n)
+ :only-of-type	
+ :only-child	
+ :optional	
+ :out-of-range	
+ :read-only	
+ :read-write	
+ :required	
+ :root	
+ :target	
+ :valid	
+ :visited

---

## pseudo-elements

> A CSS pseudo-element is used to style specified parts of an element.

```
selector::pseudo-element {
    property:value;
}
```

## All
+ after
+ before
+ first-letter
+ first-line
+ selection


```css
p::first-line {
    color: #ff0000;
    font-variant: small-caps;
}
```

```css
p::first-letter {
    color: #ff0000;
    font-size: xx-large;
}
```

### ::before and ::after

```css
h1::before {
    content: url(smiley.gif);
}
```

### ::selection

The ::selection pseudo-element matches the portion of an element that is selected by a user.

```css
::selection {
    color: red; 
    background: yellow;
}
```

---

## Opacity

The opacity property can take a value from 0.0 - 1.0. The lower value, the more transparent.

```css
img {
    opacity: 0.5;
    filter: alpha(opacity=50); /* For IE8 and earlier */
}
```

### Transparent Hover Effect

```css
img {
    opacity: 0.5;
    filter: alpha(opacity=50); /* For IE8 and earlier */
}

img:hover {
    opacity: 1.0;
    filter: alpha(opacity=100); /* For IE8 and earlier */
}
```

### Transparency using RGBA

```css
div {
    background: rgba(76, 175, 80, 0.3) /* Green background with 30% opacity */
}
```

---

## Navigation Bar

```html
<ul>
  <li><a href="default.asp">Home</a></li>
  <li><a href="news.asp">News</a></li>
  <li><a href="contact.asp">Contact</a></li>
  <li><a href="about.asp">About</a></li>
</ul>
```

### Active / Current Navigation Link

```css
.active {
    background-color: #4CAF50;
    color: white;
}
```

### Vertical Navigation Bar

```css
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    width: 200px;
    background-color: #f1f1f1;
}

li a {
    display: block;
    color: #000;
    padding: 8px 16px;
    text-decoration: none;
}

/* Change the link color on hover */
li a:hover {
    background-color: #555;
    color: white;
}
```

### Horizontal Navigaton Bar

```css
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: #333;
}

li {
    float: left;
}

li a {
    display: block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
}

/* Change the link color to #111 (black) on hover */
li a:hover {
    background-color: #111;
}
```

### Fixed Navigation Bar

```css
ul {
    position: fixed;
    top: 0;
    width: 100%;
}
```

### Responsive Topnav

```html
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {margin: 0;}

ul.topnav {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: #333;
}

ul.topnav li {float: left;}

ul.topnav li a {
    display: block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
}

ul.topnav li a:hover:not(.active) {background-color: #111;}

ul.topnav li a.active {background-color: #4CAF50;}

ul.topnav li.right {float: right;}

@media screen and (max-width: 600px){
    ul.topnav li.right, 
    ul.topnav li {float: none;}
}
</style>
</head>
<body>

<ul class="topnav">
  <li><a class="active" href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li><a href="#contact">Contact</a></li>
  <li class="right"><a href="#about">About</a></li>
</ul>

<div style="padding:0 16px;">
  <h2>Responsive Topnav Example</h2>
  <p>This example use media queries to stack the topnav vertically when the screen size is 600px or less.</p>
  <p>You will learn more about media queries and responsive web design later in our CSS Tutorial.</p>
  <h4>Resize the browser window to see the effect.</h4>
</div>

</body>
</html>
```

### Responsive Sidenav

```html
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {margin: 0;}

ul.sidenav {
    list-style-type: none;
    margin: 0;
    padding: 0;
    width: 25%;
    background-color: #f1f1f1;
    position: fixed;
    height: 100%;
    overflow: auto;
}

ul.sidenav li a {
    display: block;
    color: #000;
    padding: 8px 16px;
    text-decoration: none;
}
 
ul.sidenav li a.active {
    background-color: #4CAF50;
    color: white;
}

ul.sidenav li a:hover:not(.active) {
    background-color: #555;
    color: white;
}

div.content {
    margin-left: 25%;
    padding: 1px 16px;
    height: 1000px;
}

@media screen and (max-width: 1050px){
    ul.sidenav {
        width:100%;
        height:auto;
        position:relative;
    }
    ul.sidenav li a {
        float: left;
        padding: 15px;
    }
    div.content {margin-left:0;}
}

@media screen and (max-width: 400px){
    ul.sidenav li a {
        text-align: center;
        float: none;
    }
}
</style>
</head>
<body>

<ul class="sidenav">
  <li><a class="active" href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li><a href="#contact">Contact</a></li>
  <li><a href="#about">About</a></li>
</ul>

<div class="content">
  <h2>Responsive Sidenav Example</h2>
  <p>This example use media queries to transform the sidenav to a top navigation bar when the screen size is 1050px or less.</p>
  <p>We have also added a media query for screens that are 400px or less, which will vertically stack and center the navigation links.</p>
  <p>You will learn more about media queries and responsive web design later in our CSS Tutorial.</p>
  <h4>Resize the browser window to see the effect.</h4>
</div>

</body>
</html>
```

### Dropdown Navbar

```html
<!DOCTYPE html>
<html>
<head>
<style>
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: #333;
}

li {
    float: left;
}

li a, .dropbtn {
    display: inline-block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
}

li a:hover, .dropdown:hover .dropbtn {
    background-color: red;
}

li.dropdown {
    display: inline-block;
}

.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
}

.dropdown-content a {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
    text-align: left;
}

.dropdown-content a:hover {background-color: #f1f1f1}

.dropdown:hover .dropdown-content {
    display: block;
}
</style>
</head>
<body>

<ul>
  <li><a href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li class="dropdown">
    <a href="javascript:void(0)" class="dropbtn">Dropdown</a>
    <div class="dropdown-content">
      <a href="#">Link 1</a>
      <a href="#">Link 2</a>
      <a href="#">Link 3</a>
    </div>
  </li>
</ul>

<h3>Dropdown Menu inside a Navigation Bar</h3>
<p>Hover over the "Dropdown" link to see the dropdown menu.</p>

</body>
</html>
```

---

## Dropdowns

### Basic Dropdown

```html
<style>
.dropdown {
    position: relative;
    display: inline-block;
}

.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    padding: 12px 16px;
    z-index: 1;
}

.dropdown:hover .dropdown-content {
    display: block;
}
</style>

<div class="dropdown">
  <span>Mouse over me</span>
  <div class="dropdown-content">
    <p>Hello World!</p>
  </div>
</div>
```

[More Examples](http://www.w3schools.com/css/css_dropdowns.asp)

---

## Tooltips

### Basic Tooltips

```html
<style>
/* Tooltip container */
.tooltip {
    position: relative;
    display: inline-block;
    border-bottom: 1px dotted black; /* If you want dots under the hoverable text */
}

/* Tooltip text */
.tooltip .tooltiptext {
    visibility: hidden;
    width: 120px;
    background-color: black;
    color: #fff;
    text-align: center;
    padding: 5px 0;
    border-radius: 6px;
 
    /* Position the tooltip text - see examples below! */
    position: absolute;
    z-index: 1;
}

/* Show the tooltip text when you mouse over the tooltip container */
.tooltip:hover .tooltiptext {
    visibility: visible;
}
</style>

<div class="tooltip">Hover over me
  <span class="tooltiptext">Tooltip text</span>
</div>
```

### Tooltip Arrows

```css
/* Top Arrow */
.tooltip .tooltiptext::after {
    content: " ";
    position: absolute;
    bottom: 100%;  /* At the top of the tooltip */
    left: 50%;
    margin-left: -5px;
    border-width: 5px;
    border-style: solid;
    border-color: transparent transparent black transparent;
}
```

[Tooltip examples](http://www.w3schools.com/css/css_tooltip.asp)

---

### Image Gallery

```html
<html>
<head>
<style>
div.img {
    margin: 5px;
    border: 1px solid #ccc;
    float: left;
    width: 180px;
}

div.img:hover {
    border: 1px solid #777;
}

div.img img {
    width: 100%;
    height: auto;
}

div.desc {
    padding: 15px;
    text-align: center;
}
</style>
</head>
<body>

<div class="img">
  <a target="_blank" href="fjords.jpg">
    <img src="fjords.jpg" alt="Fjords" width="300" height="200">
  </a>
  <div class="desc">Add a description of the image here</div>
</div>

<div class="img">
  <a target="_blank" href="forest.jpg">
    <img src="forest.jpg" alt="Forest" width="300" height="200">
  </a>
  <div class="desc">Add a description of the image here</div>
</div>

<div class="img">
  <a target="_blank" href="lights.jpg">
    <img src="lights.jpg" alt="Northern Lights" width="300" height="200">
  </a>
  <div class="desc">Add a description of the image here</div>
</div>

<div class="img">
  <a target="_blank" href="mountains.jpg">
    <img src="mountains.jpg" alt="Mountains" width="300" height="200">
  </a>
  <div class="desc">Add a description of the image here</div>
</div>

</body>
</html>
```

### Responsive Image Gallery

```html
<!DOCTYPE html>
<html>
<head>
<style>
div.img {
    border: 1px solid #ccc;
}

div.img:hover {
    border: 1px solid #777;
}

div.img img {
    width: 100%;
    height: auto;
}

div.desc {
    padding: 15px;
    text-align: center;
}

* {
    box-sizing: border-box;
}

.responsive {
    padding: 0 6px;
    float: left;
    width: 24.99999%;
}

@media only screen and (max-width: 700px){
    .responsive {
        width: 49.99999%;
        margin: 6px 0;
    }
}

@media only screen and (max-width: 500px){
    .responsive {
        width: 100%;
    }
}

.clearfix:after {
    content: "";
    display: table;
    clear: both;
}
</style>
</head>
<body>

<h2>Responsive Image Gallery</h2>
<h4>Resize the browser window to see the effect.</h4>

<div class="responsive">
  <div class="img">
    <a target="_blank" href="img_fjords.jpg">
      <img src="img_fjords.jpg" alt="Trolltunga Norway" width="300" height="200">
    </a>
    <div class="desc">Add a description of the image here</div>
  </div>
</div>


<div class="responsive">
  <div class="img">
    <a target="_blank" href="img_forest.jpg">
      <img src="img_forest.jpg" alt="Forest" width="600" height="400">
    </a>
    <div class="desc">Add a description of the image here</div>
  </div>
</div>

<div class="responsive">
  <div class="img">
    <a target="_blank" href="img_lights.jpg">
      <img src="img_lights.jpg" alt="Northern Lights" width="600" height="400">
    </a>
    <div class="desc">Add a description of the image here</div>
  </div>
</div>

<div class="responsive">
  <div class="img">
    <a target="_blank" href="img_mountains.jpg">
      <img src="img_mountains.jpg" alt="Mountains" width="600" height="400">
    </a>
    <div class="desc">Add a description of the image here</div>
  </div>
</div>

<div class="clearfix"></div>

<div style="padding:6px;">
  <p>This example use media queries to re-arrange the images on different screen sizes: for screens larger than 700px wide, it will show four images side by side, for screens smaller than 700px, it will show two images side by side. For screens smaller than 500px, the images will stack vertically (100%).</p>
  <p>You will learn more about media queries and responsive web design later in our CSS Tutorial.</p>
</div>

</body>
</html>
```

---

## Image Sprites

An image sprite is a collection of images put into a single image.

A web page with many images can take a long time to load and generates multiple server requests.

Using image sprites will reduce the number of server requests and save bandwidth.

```css
#home {
    width: 46px;
    height: 44px;
    background: url(img_navsprites.gif) 0 0;
}
```

---