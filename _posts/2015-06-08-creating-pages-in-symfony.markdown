---
layout: post
title: "Creating Pages in Symfony"
date:   2015-06-08 19:45:03
categories: php symfony
---

## Create a page

Two step process

* Create a route
* Create a controller

## Environments & Front Controllers

Symfony comes with three environments defined

* dev (*app_dev.php*)
* test
* prod (*app.php*)

When running in debug mode, Symfony runs slower, but your changes are reflected  without having to manually clear the cache.

## Create the Bundle

> A bundle is nothing more than a directory that houses everything related to a specific feature, including PHP classes, configuration, and even stylesheets and JavaScript files.

example
{% highlight Bash %}
$ php app/console generate:bundle --namespace=Acme/DemoBundle --format=yml
{% endhighlight %}

Behind the scenes:

* A directory is created for the bundle at **src/Acme/DemoBundle**.
* A line is also automatically added to the **app/AppKernel.php**.

## Create the Route

By default, the routing configuration file in a Symfony application is located at *app/config/routing.yml*.

{% highlight YAML %}
# src/Acme/DemoBundle/Resources/config/routing.yml
random:
    path:     /random/{limit}
    defaults: { _controller: AcmeDemoBundle:Random:index }
{% endhighlight %}


## Create the Controller

{% highlight PHP %}
// src/Acme/DemoBundle/Controller/RandomController.php
namespace Acme\DemoBundle\Controller;

use Symfony\Component\HttpFoundation\Response;

class RandomController
{
    public function indexAction($limit)
    {
        return new Response(
            '<html><body>Number: '.rand(1, $limit).'</body></html>'
        );
    }
}
{% endhighlight %}