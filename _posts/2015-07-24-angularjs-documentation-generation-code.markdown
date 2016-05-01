---
layout: post
title:  "AngularJS Documentation Generation Code"
date:   2015-07-24 22:12:14
categories: javascript angularjs
author: Pere Pages
---

The AngularJS project uses a form of [JSDoc](http://usejsdoc.org/) for all of its documentation.

This means that all the docs are stored inline in the source code and so are kept in sync as the code changes.

#### Links

* [JSDoc](http://usejsdoc.org/)
* [Writing AngularJS Documentation](https://github.com/angular/angular.js/wiki/Writing-AngularJS-Documentation)
* [dgeni](https://github.com/angular/dgeni)
* [docular](https://github.com/Vertafore/docular)
* [How AngularJS is using Dgeni](https://github.com/angular/angular.js/tree/master/docs)
* [the dgeni-packages source, in particular the doc-processors](https://github.com/angular/dgeni-packages/)
* [Introduction video to dgeni](https://www.youtube.com/watch?v=PQNROxXajyQ&feature=youtu.be)

This is the most important link, clear example of how to do it:
* [Dgeni example](https://github.com/petebacondarwin/dgeni-example)

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## ngdoc

The flavour of jsdoc used by AngularJS is called ngdoc and is parsed by a Node.js utility called Dgeni. The documentation is best built using grunt:

```javascript
grunt package
```

> This will generate all the AngularJS distribution files and also the documentation. Look for them inside /build/docs.

## Dgeni installation

n the project you want to document you install Dgeni by running:

```bash
$ npm install dgeni --save-dev
```

This will install Dgeni and any modules that Dgeni depends upon.

## Key concepts

* Processors
* Services
* Packages

#### Processors

Building blocks of doc generation.

#### Services

Singleton helper objects.

#### Packages

Reusable component containers.

### Depency injection in Dgeni

Everything in dgeni is an injectable component created by a **factory function**:

* processors
* services
* config blocks

### Creating Packages

**processors**, **services**, **config** and **templates** are grouped into **packages**.

```javascript
var p = new Package('docPackage',['jsdoc']).
        .factory(require('./services/myService')
        .config(function(templateFinder){
                templateFinder.tempateFolders = ['./templates'];
        });
```

### Defining servicies

Simply export a factory function from a module.

```javascript
module.exports = function log(){
        return function(message){
                console.log(message);
        };
};
```

### Processors

```javascript
module.exports = function filterNgDocsProcessor(log){
        return {
                $runAfter: ['tags-parsed'],
                $runBefore: ['extracting-tags'],
                $process: function (docs){
                        var = filteredDocs = _.filter(docs, function(doc){
                                return doc.tagas.getTag('ngdoc');
                        });
                        log.debug('filtered '+(docs.length-filteredDocs.length));
                        return filteredDocs;
                }
        };
}
```

## Running dgeni

```javascript
var Dgeni = require('dgeni');
var myPackage = require('./myPackage');
var dgeni = new Dgeni([myPackage]);

dgeni.generate().then(function (){
        //...
});
```

## dgeni-packages

[dgeni-packages](https://github.com/angular/dgeni-packages)

* **base** - basic document processing
* **jsdoc** - JSDoc style @tags
* **nunjucks** - template based rendering
* **ngdoc** - processing for the AngularJS project
* **examples** - inline runnable examples (and tests)

