Syntatically Awesome StyleSheets.

Compiles to CSS and introduces programming features to CSS

```scss
`$baseFontSize: 14px;

#main
{
	h1
	{
		font-size: $baseFontiSize;
	}
}
```

```bash
npm install sass
```

```javascript
var sass = require('sass');

sass.render(sassContents, 
function (e,css) {
	console.log(css);
}
);
```

## Why Sass?

- The color problem
- The duplication problem
- The cascade problem
- The calculation problem
- The importing problem

## Using Sass

- Variables
- Rules
- Import
- Extend
- Mixin
- Function
- Control Directives

### Variables

```scss
$myColor: #ffeedd;

$a: Black; 					// Color
$b: 4px; 					// Units	
$c: 1.0em; 					// Units
$d: Helvetica, sans-serif; 	// Lists
$e: 1px #000 Solid 0 0; 	// Also Lists
```

#### Operations

```scss
font-size: 4px + 4; 		// 8px
font-size: 20px * .8; 		// 16px
color: #FFF / 4; 			// #404040
width: (100% / 2) + 25%;	// 75%
```

#### Color Functions

```scss
color: lighten($color, 10%);
color: darken($color, 10%);

color: saturate($color, 10%);
color: desaturate($color, 10%);

color: fade_in($color, .1);
color: fade_out($color, .1);

color: invert($color);
color: complement($color);
```

### Rules
### Import
### Extend
### Mixin
### Function
### Control Directives

