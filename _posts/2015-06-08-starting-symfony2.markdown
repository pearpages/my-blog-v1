---
layout: post
title: "Starting Symfony2"
date:   2015-06-08 19:18:03
categories: php symfony
---

## Symfony Distributions

* Symfony Standard Edition
* [Symfony CMF Standard Edition](https://github.com/symfony-cmf/symfony-cmf-standard)
* [Symfony REST Edition](https://github.com/gimler/symfony-rest-edition)

## Installing Symfony

### With Installer

```bash
c:\> php -r "readfile('http://symfony.com/installer');" > symfony

# Windows
c:\> cd projects/
c:\projects\> php symfony new my_project_name
```

### With Composer

```bash
composer create-project symfony/framework-standard-edition my_project_name
```

## Checking Symfony Version

```bash
$ php app/console --version
```

## Running the Symfony Application

```bash
$ php app/console server:run #start
$ php app/console server:stop #stop

$ php app/console cache:clear --env=prod --no-debug #prod environment
```

So for accessing dev
http://localhost/app_dev.php/random/10

For accessing prod
http://localhost/app.php/random/10

## Updating symfony
```bash
$ php composer update
```

## Checking Security Issues
```bash
$ php app/console security:check
```

## Using Git

Simfony applications already contain a **.gitignore** file.

When using Composer to manage dependencies, it is recommended to ignore the entire **vendor/** directory before committing its code to the repository. 

When cloning from git we need to install the *vendor* files
```bash
$ composer install
```
