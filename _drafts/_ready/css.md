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

