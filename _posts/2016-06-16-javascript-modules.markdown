---
layout: post
title: "JavaScript Modules"
date:   2016-06-16 08:33:12
categories: javascript modules
author: Pere Pages
---

#### Contents
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

It's all about letting webpack know how to get the dependencies.

```bash
npm install angular webpack babel-loader raw-loader -D
```

The whole point is that the app requires the modules, and the modules require its functionalities so the dependencies don't break.

Being ```index.js``` the entry point for webpack.

```js
// index.js
var angular = require('angular');
var app = angular.module('app',[]);

require('./bands')(app); // we are rquiring the index.js
```

Bands one of the modules we've created

```js
// bands/index.js

module.exports = function(app) {
    require('./band-info')(app);
    require('./bandList')(app);
}
```

```js
//  bands/band-info.js
module.exports = function(app) {
    app.directive('bandInfo', function(bandList) {
        return {
            template: require('./band-info.html'), // see how we are including the html template
            restrict: 'E',
            controller: function($scope) {
            }
        }
    });
}
```

```html
// bands/band-info.html

<!— whatever html —>
```

```js
// bands/bandList.js

module.export = function(app) {
    app.factory('bandList', function() {
        return // ...
    }
}
```