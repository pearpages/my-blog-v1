---
layout: post
title:  "Karma Code Coverage with Istanbul"
date:   2015-07-24 20:33:15
categories: javascript karma istanbul
---

Karma can generate code coverage using awesome Istanbul. If you want to generate the coverage, you need to configure up to three parts:

* preprocessor coverage (required)
* reporter coverage (required)
* reporter options (optional)

#### Links

[Karma docs](http://karma-runner.github.io/0.8/config/coverage.html)


#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Preprocessor

The preprocessor configures which files should be tested for coverage.

{% highlight javascript %}
preprocessors = {
  'www/js/**/*.js': 'coverage'
};
{% endhighlight %}

### Important

**You should not however include the files that aren't directly related to your program, e.g. libraries, mocks, neither tests.**

## Reporter

To activate the coverage reporter add this to your configuration file.

{% highlight javascript %}
        reporters = ['coverage'];
{% endhighlight %}

This will create a coverage report for every browser that the tests are run in. In addition, it will create a JSON file that outputs the intermediate data.

## Reporter Options

The reporter defaults to the following values.

{% highlight javascript %}
coverageReporter = {
  type : 'html',
  dir : 'coverage/'
}
{% endhighlight %}

## Other

To make it work I needed to change the **karma.conf.js**.

{% highlight javascript %}
// the plugins I am pusing
plugins: [
      "karma-phantomjs-launcher",
      "karma-jasmine",
      "karma-coverage"
    ],
{% endhighlight %}

Obviously installing everything

{% highlight bash %}
$ npm install -g istanbul
$ npm install -g karma-coverage
{% endhighlight %}