---
layout: post
sidebar-align: left
title: "Creating Pages in Symfony"
date:   2015-06-08 19:45:03
categories: php symfony
author: Pere Pages
---

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Create a page

Two step process

* Create a route
* Create a controller
* Create the template (optional)

## Environments & Front Controllers

Symfony comes with three environments defined

* dev (*app_dev.php*)
* test
* prod (*app.php*)

When running in debug mode, Symfony runs slower, but your changes are reflected  without having to manually clear the cache.

## Create the Bundle

> A bundle is nothing more than a directory that houses everything related to a specific feature, including PHP classes, configuration, and even stylesheets and JavaScript files.

example
```bash
$ php app/console generate:bundle --namespace=Acme/DemoBundle --format=yml
```

Behind the scenes:

* A directory is created for the bundle at **src/Acme/DemoBundle**.
* A line is also automatically added to the **app/AppKernel.php**.

## Create the Route

By default, the routing configuration file in a Symfony application is located at *app/config/routing.yml*.

```yaml
# src/Acme/DemoBundle/Resources/config/routing.yml
random:
    path:     /random/{limit}
    defaults: { _controller: AcmeDemoBundle:Random:index }
```


## Create the Controller

```php
<?php
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
```

## Create the template

```php
<?php
// src/Acme/DemoBundle/Controller/RandomController.php
namespace Acme\DemoBundle\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\Controller;

class RandomController extends Controller
{
    public function indexAction($limit)
    {
        $number = rand(1, $limit);

        return $this->render(
            'AcmeDemoBundle:Random:index.html.twig',
            array('number' => $number)
        );

        // render a PHP template instead
        // return $this->render(
        //     'AcmeDemoBundle:Random:index.html.php',
        //     array('number' => $number)
        // );
    }
}
```

Paying attention to:
```php
<?php
return $this->render(
            'AcmeDemoBundle:Random:index.html.twig',
            array('number' => $number)
        );
```

**AcmeDemoBundle:Random:index.html.twig**

> BundleName:ControllerName:TemplateName

> /path/to/BundleName/Resources/views/ControllerName/TemplateName

```php
<!-- src/Acme/DemoBundle/Resources/views/Random/index.html.php -->
<?php $view->extend('::base.html.php') ?>

Number: <?php echo $view->escape($number) ?>
```



```php
<!-- app/Resources/views/base.html.php -->
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title><?php $view['slots']->output('title', 'Welcome!') ?></title>
        <?php $view['slots']->output('stylesheets') ?>
        <link rel="shortcut icon"
            href="<?php echo $view['assets']->getUrl('favicon.ico') ?>" />
    </head>
    <body>
        <?php $view['slots']->output('_content') ?>
        <?php $view['slots']->output('javascripts') ?>
    </body>
</html>
```

## The Directory Structure

Symfony projects are structured and organized.

* app/
        *This directory contains the application configuration.*
* src/
        *All the project PHP code is stored under this directory.*
* vendor/
        *Any vendor libraries are placed here by convention.*
* web/ 
        *This is the web root directory and contains any publicly accessible files.*

The **web** root directory is the home of all public and static files including images, stylesheets, and JavaScript files. It is also where each front controller lives:

The front controller file (**app.php** in this example) is the actual PHP file that's executed when using a Symfony application and its job is to use a Kernel class, **AppKernel**, to bootstrap the application.

## The Application (app) Directory

###AppKernel

* registerBundles()
* registerContainerConfiguration()

### Day-to-day development

* app/config/ *to modify configuration and routing files**
* app/cache/
* app/logs/
* app/Resources/ *templates, ..*

### Autoloading

>  Composer uses the namespace of a class to determine its location and automatically includes the file on your behalf the instant you need a class.

The class name and path to the file have to follow the same pattern:

```php
Class Name:
    Acme\DemoBundle\Controller\RandomController
Path:
    src/Acme/DemoBundle/Controller/RandomController.php
```

## What is a bundle?

A bundle is simply a structured set of files within a directory that implement a single feature. You might create a BlogBundle, a ForumBundle or a bundle for user management (many of these exist already as open source bundles). Each directory contains everything related to that feature, including PHP files, templates, stylesheets, JavaScripts, tests and anything else. Every aspect of a feature exists in a bundle and every feature lives in a bundle.

> A bundle can live anywhere as long as it can be autoloaded (via the autoloader configured at *app/autoload.php*).

## Creating a Bundle

```php
<?php
// src/Acme/TestBundle/AcmeTestBundle.php
namespace Acme\TestBundle;

use Symfony\Component\HttpKernel\Bundle\Bundle;

class AcmeTestBundle extends Bundle
{
}
```

### Registering the Bundle

```php
<?php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        // ...
        // register your bundle
        new Acme\TestBundle\AcmeTestBundle(),
    );
    // ...

    return $bundles;
}
```

### Creating the Bundle automatically

```bash
$ php app/console generate:bundle --namespace=Acme/TestBundle
```

This does

* creates a basic controller
* template
* routing

But you still have to **register** the bundle!

## Bundle Directory Structure

* Controller/
* DependencyInjection/ *(this directory is not necessary) Might hold classes for importing service configuration, register compiler passes or more.*
* Resources/config/ *includes routing*
* Resources/views/ 
* Resources/public/ *images, stylesheets* **It is copied or symbolically linked into the project **web/** directory via the **assets:install** console command.
* Tests/

## Default Configuration Dump

```bash
$ app/console config:dump-reference FrameworkBundle
# The extension alias (configuration key) can also be used:
$ app/console config:dump-reference framework
```

## Environments

* dev
* test
* prod

> Since the prod environment is optimized for speed; the configuration, routing and Twig templates are compiled into flat PHP classes and cached. When viewing changes in the prod environment, **you'll need to clear these cached files** and allow them to rebuild:

```php
$ php app/console cache:clear --env=prod --no-debug
```

> The **test** environment is used when running automated tests and **cannot be accessed directly through the browser**.

### Configuration

The **AppKernel** class is responsible for actually loading the configuration file of your choice.
```yaml
# app/config/config_dev.yml
imports:
    - { resource: config.yml }

framework:
    router:   { resource: "%kernel.root_dir%/config/routing_dev.yml" }
    profiler: { only_exceptions: false }

# ...
```