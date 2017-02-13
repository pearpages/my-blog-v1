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

## Tables

