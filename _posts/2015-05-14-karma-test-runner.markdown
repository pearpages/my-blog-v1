---
layout: post
title:  "Karma Test Runner"
date:   2015-05-14 00:00:12
---

Karma is a test runner based on Node.js. 

The Karma team recommends installing Karma **locally at the project level**. So, we are supposed to add it in the *package.json* file of each of our projects.

Karma will be located under the *node_modules* folder within our project. Any other Node.js dependencies defined in the *package.json* file will also be located under the *node_modules* folder.

## karma.conf.js

Karma requires a configuration file named *karma.conf.js*

{% highlight javascript %}
module.exports = function (config){
        config.set({
            basePath: '../',
            files: [],
            exclude: [],
            autoWatch: true,
            frameworks: [],
            browsers: [],
            plugins: []
        });
}
{% endhighlight %}