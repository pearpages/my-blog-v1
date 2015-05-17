---
layout: post
title:  "Notes on creating an app"
date:   2015-05-17 22:10:02
categories: javascript app
---

## Features

We need to detail the features that the app supports.

Once we have the feature list, we can now determine what data needs to be tracked and that becomes part of our model.

So it is very important to first think aobut the functionality and then the model to support it. Finally how to build the view for it.

## About the Viewport

> A typical mobile-optimized site contains something like the following:

{% highlight html %}
<meta name="viewport" content="width=device-width, initial-scale=1">
{% endhighlight %}

> The width property controls the size of the viewport. It can be set to a specific number of pixels like width=600 or to the special value device-width value which is the width of the screen in CSS pixels at a scale of 100%. (There are corresponding height and device-height values, which may be useful for pages with elements that change size or position based on the viewport height.)

> The initial-scale property controls the zoom level when the page is first loaded. The maximum-scale, minimum-scale, and user-scalable properties control how users are allowed to zoom the page in or out.

