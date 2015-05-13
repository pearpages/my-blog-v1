---
layout: post
title:  "Protractor"
date:   2015-05-14 00:00:25
categories: javascript tests framework
---

Protractor is a **Node.js-based** framework, just like Karma.

Protractor is build on top of **WebDriverJS**. The Protractor team recomends installing it **globally** on your system.

{%highlight javascript %}
npm install -g protractor
//g for globally

//since protractor is built on WebDriverJS, we must also configure WebDriverJS
webdriver-manager update

//start the Selenium Server that WebDriverJS usese to run Protractor test scripts
webdriver-manager start
{% endhighlight %}

## conf.js

{%highlight javascript %}
exports.config = {
	seleniumAddress: 'http//localhost:4444'/wd/hub',
	specs: ['blog-spec.js']
};

//we need to create the blog-spec.js with the tests

//then we run
protractor conf.js
{% endhighlight %}

Protractor can be integrated with *continous integration* (CI) build systems like Travis CI and Jenkins.