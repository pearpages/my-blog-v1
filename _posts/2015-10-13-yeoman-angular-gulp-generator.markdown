---
layout: post
sidebar-align: left
title:  "Angular Gulp Generator"
date:   2015-10-13 19:52:33
categories: javascript angularjs yeoman generator
author: Pere Pages
---

Lets you quickly set up a project with:

+ with popular technologies
+ web best pratices.
+ guidelines powered by Google.

#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Usage

### Install & Run

```bash
# Installing yeoman, gulp and bower
$ npm install -g yo gulp bower

# Installing the generator
$ npm install -g generator-gulp-angular

# run
yo gulp-angular
```

## Yo options
`yo gulp-angular --help` or `yo gulp-angular -h` for help. All options are not required. If not provided, default values will be used.

* `--app-path='src'` customize Angular's app folder, relative to cwd, default is `src`
* `--dist-path='dist'` customize build target folder, relative to cwd, default is `dist`
* `--e2e-path='e2e'` customize e2e test specs folder, relative to cwd, default is `e2e`
* `--tmp-path='.tmp'` customize pre-processing temp folder, relative to cwd, default is `.tmp`
* `--skip-install` do not run `bower install` and `npm install` after generating the app, default is `false` (not skip)
* `--skip-welcome-message` skip yo welcome messages, default is `false` (not skip)
* `--skip-message` skip install messages, default is `false` (not skip)
* `--default` use default configurations, default is `false`
* `--advanced` prompt for advanced additional features, default is `false`


Paths configuration are stored in `gulpfile.js`. Change `options.(src|dist|tmp|e2e)` in `gulpfile.js` if you want to config paths after the app is generated.

**Warning**: The paths are also written in the `index.html` for the build with useref. If you want to change these paths, you also have to change the paths there in order to have the build task working.

## Use Gulp tasks

* `gulp` or `gulp build` to build an optimized version of your application in `/dist`
* `gulp serve` to launch a browser sync server on your source files
* `gulp serve:dist` to launch a server on your optimized application
* `gulp test` to launch your unit tests with Karma
* `gulp test:auto` to launch your unit tests with Karma in watch mode
* `gulp protractor` to launch your e2e tests with Protractor
* `gulp protractor:dist` to launch your e2e tests with Protractor on the dist files

More information on the gulp tasks in the [User Guide](user-guide.md).

## Directory structure

[Best Practice Recommendations for Angular App Structure](https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/pub)

The root directory generated with default paths configuration for application with name `gulpAngular`:
<pre>
├──  bower_components/
├──  e2e/
├──  gulp/
├──  nodes_modules/
│
├──  src/
│   ├──  app/
│   │   ├──  components/
│   │   │   └──  githubContributor/
│   │   │   │   └──  githubContributor.service.js
│   │   │   │
│   │   │   └──  malarkey/
│   │   │   │   ├──  malarkey.directive.js
│   │   │   │   └──  malarkey.(scss|styl|less|css)
│   │   │   │
│   │   │   └──  navbar/
│   │   │   │   ├──  navbar.directive.(js|ts|coffee)
│   │   │   │   ├──  navbar.html
│   │   │   │   └──  navbar.(scss|styl|less|css)
│   │   │   │
│   │   │   └──  webDevTec/
│   │   │       └──  webDevTec.service.js
│   │   │
│   │   ├──  main/
│   │   │   ├──  main.controller.(js|ts|coffee)
│   │   │   ├──  main.controller.spec.js
│   │   │   └──  main.html
│   │   │
│   │   └──  index.config.(js|ts|coffee)
│   │   └──  index.constants.(js|ts|coffee)
│   │   └──  index.module.(js|ts|coffee)
│   │   └──  index.route.(js|ts|coffee)
│   │   └──  index.run.(js|ts|coffee)
│   │   └──  index.(scss|styl|less|css)
|   |
│   ├──  assets/
│   │   └──  images/
│   ├──  favico.ico
│   └──  index.html
│
├──  .bowerrc
├──  .editorconfig
├──  .gitignore
├──  .eslintrc
├──  bower.json
├──  gulpfile.js
├──  karma.conf.js
├──  package.json
└──  protractor.conf.js
</pre>

There is none at the generation but you can add `.jade`, `.haml` or `.hbs` (dependent of your HTML pre-processor choice) anywhere in the `src` folder and it will be compiled automatically. **Warning**, the first file of a type in a folder is often missed by the Gulp watch, try to relaunch Gulp if it happens.


## Features included in the gulpfile
* *useref* : allow configuration of your files in comments of your HTML file
* *ngAnnotate* : convert simple injection to complete syntax to be minification proof
* *uglify* : optimize all your JavaScript
* *csso* : optimize all your CSS
* *rev* : add a hash in the file names to prevent browser cache problems
* *watch* : watch your source files and recompile them automatically
* *eslint* : The pluggable linting utility for JavaScript
* *imagemin* : all your images will be optimized at build
* *Unit test (karma)* : out of the box unit test configuration with karma
* *e2e test (protractor)* : out of the box e2e test configuration with protractor
* *browser sync* : full-featured development web server with livereload and devices sync
* *angular-templatecache* : all HTML partials will be converted to JS to be bundled in the application
* **TODO** lazy : don't process files which haven't changed when possible


## Questions the generator will ask
* *jQuery*: jQuery 1.x, 2.x, Zepto, none
* *Angular modules*: animate, cookies, touch, sanitize
* *Resource handler*: ngResource, Restangular, none
* *Router*: ngRoute, UI Router, none
* *UI Framework*: Bootstrap, Foundation, Angular Material, Material Design Lite, none (depends on the chosen CSS preprocessor)
* *UI directives* : UI Bootstrap, Angular Strap, official Bootstrap JavaScript, Angular Foundation, official Foundation JavaScript, none (depends on the UI framework)
* *CSS pre-processor*: Less, Sass with Ruby and Node, Stylus, none
* *JS preprocessor*: CoffeeScript, TypeScript, ECMAScript 6 (Traceur and Babel), none
* *HTML preprocessor*: Jade, Haml, Handlebars, none
* **TODO** Script loader: Require, Webpack, none
* **TODO** Test framework: Jasmine, Mocha, Qunit

## Recipes

The community has written [recipes](recipes#recipes) for common use-cases that we chose not to add as a feature of the generator.

- [Accessing 'bower_components' in .scss files without having to path ../../bower_components/](recipes/accessing-bower-components-scss.md)
- [How to add fontawesome?](recipes/add-fontawesome.md)
- [How to add gulp-react to a project?](recipes/add-gulp-react.md)
- [Build without concat CSS files](recipes/build-without-concat-css.md)
- [Is there a way to change the output directory of fonts, scripts and styles?](recipes/change-dist-file-names.md)
- [How can I have an environment specific build?](recipes/environment-specific-build.md)
- [How can exclude some HTML files from being added to the Angular cache?](recipes/keep-some-html-files-in-dist.md)
- [Where to place third-party files?](recipes/managing-third-party-files.md)
- [How shall I properly upgrade my current project with the last version of the generator?](recipes/upgrade-my-current-project.md)
- [Use spritesheets](recipes/use-spritesheet.md)

## User Guide

You've just generated a brand new project which is full of useful features, here's an introduction to what you have.

## Yeoman Workflow

We're proud to say that this generator follows the Yeoman generator guidelines by the book.

### `serve`

For the development phase, the command `gulp serve` launches a server which supports live reload of your modifications.

Its usage is described in the chapters [Development server](#development-server) and [File watching & pre-processing](#file-watching--pre-processing)

### `test`

For testing, a fully working test environment is shipped with some examples. It uses Karma (with `gulp test`) for the unit tests, and Protractor for the end-to-end tests (with `gulp protractor`).

More information in the [Test environment configured](#test-environment-configured) chapter.

### `build`

The generator brings a state of the art optimization process with the command `gulp build` or simply `gulp`. It's fully described in the [Optimization process](#optimization-process) chapter.

### `inject`

This generator goes further than the Yeoman guidelines by shipping a fully working file injection process which is able to automatically write all of your `script` and `link` tags in your `index.html`

All the details about how to use injection are in the [File injection](#file-injection) chapter.

## Development server

The generator is shipped with the awesome [Browser Sync](http://www.browsersync.io/) as the development server.

The recommended development process is to serve your web resources locally to be more reactive and be able to have features like automatic reload of your page when you make a modification.

If you have a backend server to address, keep the development server and either:
  - launch your request with complete URLs (but you'll have to handle [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)) 
  - or you can use the embedded proxy feature which can redirect your request from the development server to your backend transparently without dealing with CORS.

### Serve you `src` folder

Browser Sync is configured to serve your `src` folder. Or at least all the files not transformed in `src`.

For the pre-processed files (depending of your options, could be all your files), Browser Sync is configured to also serve the `.tmp/serve` folder.

With the [file watching and pre-processing](#file-watching--pre-processing) feature, your files will be automatically processed and put in the `.tmp/serve` folder. This process should be transparent.

If the same file is in both directories, the one in `.tmp/serve` will be chosen.

Finally, your `bower_components` folder, which contains your external dependencies from Bower (and is not located inside the `src` folder), will be served with the `bower_components` alias at the root of the server.

### Live reload of your sources

When you launch your dev. server with `gulp serve`, it will launch Browser Sync along with the [file watching and pre-processing](#file-watching--pre-processing) feature.

When gulp detects a change, it will send a reload command to Browser Sync. Depending on which files have changed (html/js or css) it will reload the whole page or just reload the css and keep your page context up.

### The proxy feature

As mentioned in the introduction, it's considered a good process to keep using the dev server even if you also have a backend running on your computer.

At this point, your application will have to launch requests both to request static files of the front end project, and dynamic routes of your backend.

The cleaner way to address this need is to add a proxy feature to the Browser Sync server. This feature is inactive by default as we can't know about your backend configuration, but it's in the comments and easy to start. Look in `gulp/serve.js`, you've got a line in the comments:
```javascript
server.middleware = proxyMiddleware('/users', {target: 'http://jsonplaceholder.typicode.com', proxyHost: 'jsonplaceholder.typicode.com'});
```

Replace the parameters with your needs, relaunch the server, and you should be able to target your backend through Browser Sync's domain and port.

If you want more detail about the proxy middleware, look at the external lib which provides the feature: https://github.com/chimurai/http-proxy-middleware

## File watching & pre-processing

When you run the dev. server or if you manually launch the `watch` task, Gulp will watch your changes on the files in the `src` folder. This enables Gulp to launch all processings on your file as soon as you hit save.

All processings are watching your `src` directory and put their results in the `.tmp/serve` folder. **There is no automatic process featured in the generator which will modify your files in the `src` folder**. The processed version of the files are written at the same path as the original file with often a new file extension.

There are 4 processings featured in the generator:
- **Injection** (`gulp/inject.js`): When you put any files ending by `.js` or `.css` in your `src` folder or when you add a Bower dependency, it will rewrite a new `index.html`, more information in the [file injection chapter](#file-injection)
- **Scripts** (`gulp/scripts.js`): If you choose a script pre-processor, all modification or creation on your files matching the extension of your pre-processor will trigger a recompile.
- **Styles** (`gulp/styles`): If you choose a CSS pre-procesor, all modification or creation on your files matching the extension of your pre-processor will trigger a recompile.
- **Markups** (`gulp/markups`): If you choose an HTML pre-procesor, all modification or creation on your files matching the extension of your pre-processor will trigger a recompile.

**Warning**: The generator uses the file watching from Gulp 3 which is known to have some limitations. For example a new directory or the creation of the first file in a directory will be missed. Please try to stop your watch process and relaunch it before asking for help.

There are gulp plugins to address this problem but we agreed on staying as it is waiting for the release of Gulp 4 which will fix these problems

## File injection

If you open your generated `index.html` you'll see that it's full of comments and that there is no (or very few) `script` and `link` tags.

It's because this generator has an automatic process which will write them for you. It will not rewrite your `src/index.html` as it would be changing your sources. It will put the **injected** version in the `.tmp/serve` folder.

There is two types of file injection which will be performed, the injection of your external dependencies from Bower and the injection of your source files discovered in the `src` folder.

### Bower dependencies

An external tool called [Wiredep](https://github.com/taptapship/wiredep) is used in the generated project to list the Bower dependencies and inject them in the index.html.

You have to notice that in order to work correctly, your Bower dependencies should be listed in the `bower.json`, installed in the `bower_components` folder and contains a `bower.json` of their own listing the files to include in the property `main`.

A dependency wrongly installed or which doesn't link properly the files to include in its `bower.json` (not yours, the one of the lib) will not be injected properly. If this appens, you have a way to include manually files described in the chapter [Manual injection](#manual-injection).

### Your source code

The generator is also abled to automatically write the `script` and `link` tags for your own source files. To do that, it looks through the whole content of the `src` folder and inject all the files in the `index.html`.

As the order of the files are important in JavaScript, the order is not chosen randomly. We use a script called [Angular FileSort](https://github.com/klei/gulp-angular-filesort) which will analyse your source code and reorder your files respecting the dependencies discovered through the Angular modules.

For the CSS, the order is not important. Unfortunately for the CSS pre-processors the order does matters but we don't have any ordering feature to solve the issue. The only element we can give is that the order is not random but depends on the folder structure and the file names and in most of the case it's possible to find a structure which will assure the files to be loaded in the right order.

### CSS pre-processor injection

When you use a CSS pre-processor, the inject process for your style files is a bit different. It's in the pre-processor file that you want the injection and not in the `injex.html` and it's what the injection will do.

In this special case, the "injection" will not be performed in the `inject` task or in the `index.html` file but directly in the `styles` task. You'll find comments in your `index.(scss|less|styl)` file which locate the position to add include statements with the syntax of the pre-processor.

Bower support linking dependency of CSS preprocessed files, the generated project take advantage of it and will be able to add include statements of your dependencies if they are defined properly in the bower description file of your library.

### Manual injection

We do all that we can for the process of automatic injection to be as transparent as possible and works as you could imagine it will when you modify your project.

Unfortunately there is always cases where the right inclusions are not done automatically. The most common case is the Bower dependency which doesn't defines the right files to include in its own descriptor.

It could not be obvious at the first look at the `src/index.html` you are still allowed to put your own `script` or `link` tag and load whatever you want! The key to do it right is to put your tags in the right place.

In the `index.html` file, you'll find two types of comments, some for the build process like `<!-- build:js(src) scripts/vendor.js -->` and some for the injection process like `<!-- bower:js -->` or `<!-- inject:js -->`. You'll see that injections comments are always put inside build ones because we want the inclusions to be made where the optimization process will be able to find them.

**The key is to put your tags inside the build blocks to be part of the optimization process but outside of the inject blocks which will be overriden**.

## Test environment configured

One of the goals of the generator is to bring to you a test environment already configured so you have only to write your tests.

As it is today the guideline, the tests files are placed directly in the source folder next to the file you want to test. The distinction used to separate source and test is on the file extension: `*.spec.js` and `*.mock.js`.

The `karma.conf.js` file delivered with the project is plugged with the same features and configurations than the Gulp scripts. The [File injection](#file-injection) used to populate the `index.html` file is used with the same behaviors to parameter karma.

By default, we chose to use [PhantomJS](http://phantomjs.org/) as test browser, it's shipped inside the NPM install you performed after generating the files so you don't have to have it installed in global. There is an exception when you use Traceur as JS pre-processor as they are incompatible, we switch to Chrome.

Still as default choice, the test framework is [Jasmine](http://jasmine.github.io/). It would be perfect if it was an option to choose another one in the generator but it's not the case at this point.

To allow tests to load HTML partials especially for the directives tests, we use a Karma plugin [karma-ng-html2js-preprocessor](https://github.com/karma-runner/karma-ng-html2js-preprocessor).

Other than that, we try to use as less Karma plugins as possible because they often duplicate process we already have inside Gulp. For sake of coherence and stability we're searching for a process centralized in Gulp and not duplicated in Karma or other tools like perhaps Webpack.

## Optimization process

The central piece of the optimization process is the use of the [gulp-useref](https://github.com/jonkemp/gulp-useref). Its task is to concat files and rewriting the `index.html` file to points on the concat versions of the files. All works with HTML comments block starting with `<!-- build:(...) ->` and ending with `<!-- endbuild -->`.

The plugin allows us to have gulp filters to apply transformations for the different kind of files. So the build task filter the script files then apply the optimizations transformations like [Uglify](https://github.com/mishoo/UglifyJS2) and then use the styles files and do the same for the styles.

The second important plugin used is [gulp-rev](https://github.com/sindresorhus/gulp-rev) which appends the content hash of the generated file names in order to prevent all cache problems when you deliver a new version.

The optimization process is configured (through the comments in `index.html`) to produced two JavaScript files, one for your libraries and another for your sources. It also produces one CSS file (we used to generate two like for the scripts but it created some problems).

All the HTML partials found in the sources are transformed in JavaScript with the plugin [gulp-angular-templatecache](https://github.com/miickel/gulp-angular-templatecache) and put in the sources bundle in a way which should be totally transparent for the Angular app.

All the "other" files which are not processed by any mechanism should be copied in the `dist` folder with the same path by the task `other`.

# How it Works

This document aims to explain all mechanisms included in the project generated from this generator.

When you have a problem or want to understand why it's working, check this file to try to understand what's happening.

## `gulpfile.js`

As the gulpfile was becoming enormous, we decided to split it up into several files inside the `gulp` directory. Now, the gulpfile does nothing more than loading all `.js` or `.coffee` files inside the `gulp` directory.

It only defines one task which is the default one which will be launched if you pass no arguments to the gulp command. It will be the `clean` task followed by the `build`.

## `gulp/conf.js`

The conf module doesn't define any gulp tasks. It's there to define some global values used across multiple gulp files.

We don't abuse of global configurations as a respect of the Gulp main principal **Code over configuration** (and also because we're still a bit traumatized by Grunt) but still there is the need of some global values such as:

- **paths**: main paths of the project such as `src` and `.tmp`.
- **wiredep**: wiredep is used in several tasks and needs to be configured the same way in all tasks.
- **errorHandler**: the main weakness of Gulp 3 is the error handler, we keep a centralized error handler implementation here.


## `gulp/inject.js`

The `inject` task is intended to centralized all modifications on the `index.html` of your project in the development phase. As we propose today a complete system of injection of all your files, there is several steps to organize.

As we never want to modify a source file, the injected `index.html` is targeted inside the temporary folder. You could look there to check if the changes are ok.

The task is organized by preparing first all settings of the injections the making the changes in one Gulp stream at the end.

The 3 steps of injections are:

- **Inject styles**: use of [gulp-inject](https://github.com/klei/gulp-inject) to list all the CSS files inside the head of the page.
- **Inject scripts**: use of [gulp-inject](https://github.com/klei/gulp-inject) to list all the JS files inside the body of the page (below the app).
- **Wiredep**: use of [wiredep](https://github.com/taptapship/wiredep) streams to add CSS and JS files of the Bower dependencies.

### Listing and ordering files for injection

For the first 2 tasks of injection. When you use plain JS, the list is made by listing the `src` folder. When there are pre-processing, the transformations are launched before (the `inject` task depends on `scripts` and `styles`) and the injection are performed after by listing the `tmp/serve` folder.

As the script files has to be sorted in order to work. We use a magic script which analyze the content of files and order them following the Angular modules declaration. It's used at the end of the inject stream just before writing. Warning, this plugin requires to have the content of the files and fail if you use the `{read: false}` option from `gulp.src`.

### Locating places in the `index.html`

[gulp-inject](https://github.com/klei/gulp-inject) put the `<script>` of `<link>` tags insides comments starting by `<!-- inject:css -->` or `<!-- inject:js -->` and ending by `<!-- endinject -->`.

[wiredep](https://github.com/taptapship/wiredep) put the `<script>` of `<link>` tags insides comments starting by `<!-- bower:css -->` or `<!-- bower:js -->` and ending by `<!-- endbower -->`.

Don't put anything inside this comments in your sources because the `inject` task will override it without warning you.


## `gulp/scripts.js`

The `scripts` task is launched at build, dev and test time and at the watch of any change on a script file. It's this task which will trigger a Browser Sync reload when needed.

### With no JS preprocessor

When you don't have JS preprocessor, the `scripts` task goal is to pass the linter (ESLint) on your code.

### With Coffee

This task will launch the CoffeeLint analyze and the Coffee compilation and put result files in the `.tmp/serve` folder.

### With TypeScript

The `scripts` task has a dependency which is the installation of typings with the `tsd:install` gulp task. Once the typings ready, TSLint, TypeScript compilation and finally a concatenation of all JavaScript files produced in the right order are done.

`tsd:install` is located in the `gulp/tsd.js` which is created only when choosing TypeScript. It will automatically download typings files for the dependency found in Bower with a popular library [TSD](http://definitelytyped.org/tsd/)

### With ES6

The `scripts` task changes a bit for ES6 to handle CommonJS modularization used by the ES6 preprocessors. The standard gulp stream is replaced by Webpack through its stream feature. It's Webpack which become responsible for compilation, sourcemap and linting.

As Webpack as a good watch feature, 2 tasks are produced: `scripts` and `scripts:watch`. In the second we delegates to Webpack the watching of the source script files.


## `gulp/styles.js`

The `styles` task is launched at build, dev and test time and at the watch of any change on a style file. It's this task which will trigger a Browser Sync reload when needed.

This file exists only if you choose a style pre-processor.

### Injection

As all styles pre-processors handle themselves the inclusions of all dependency files, as an exception, the style task is part of the injection process.

Like in the [`gulp/inject.js`](#gulpinjectjs), there is two kinds of injection, first, your files and the one from Bower dependencies. Still like in the standard injection, it's controlled by comments but this time in the format of the pre-processor: `// bower:(scss|less|styl)` -> `// endbower` & `// injector` -> `// endinjector`.

The injection is on step of the main Gulp stream for the styles. Once processed, the uniq file inside `.tmp/serve` will follow the standard injection process to be included in the `index.html`.

### Style stream

All transformations are made in a single stream. As it includes injection and pre-processing, it could be disturbing because there is no work files but this is the magic and power of Gulp! If you intend to debug or understanding the process, the better way is to comment one or several transformations of the stream to look at single step.

The stream by itself is composed of some very identifiable steps:
- Injection with [gulp-inject](https://github.com/klei/gulp-inject)
- Injection with [Wiredep](https://github.com/taptapship/wiredep)
- Start of sourcemap
- Style pre-processing with one of the one supported: Sass, Less or Stylus
- Autoprefixer with [gulp-autoprefixer](https://github.com/sindresorhus/gulp-autoprefixer)
- End of sourcemap
- Writing files in `.tmp/serve`
- Reloading files in Browser Sync if present

### Ruby Sass

Ruby Sass (the original implementation) caused us some pains fitting in the process. The Gulp plugin is a bit "touchy" (it's not supporting Gulp sourcemap system for example) and the options are not the same as for [node-sass](https://www.npmjs.com/package/node-sass).

In order to have the sourcemaps working, there is some exceptions. The main trick is to ask Ruby Sass to generate its own sourcemaps and then, load them with Gulp with `$.sourcemaps.init({ loadMaps: true })` and continue the normal process.


## `gulp/markups.js`

The generator handles template pre-processing even if there is no "examples" in the created project (only because it's a lot of work to maintain all versions).

When a HTML pre-processor is chosen, the `markups` task is inserted and works the same as `styles` and `scripts` one.

The transformation is handled by [Consolidate](https://github.com/tj/consolidate.js) the reference library which also handle template processing inside [Express](http://expressjs.com/).

## `gulp/watch.js`

You can use the `watch` task directly if you just want the pre-processing of your files to be triggered automatically but it's mainly used through Browser Sync with the `server` task.

The `watch` task is responsible for watching all the files of the project in order to relaunch all the processings needed.

### Standard Gulp watch

We intentionally kept using the official Gulp watch even if we know that it has some weakness (first file of a directory not seen for example). But we know that there is some external lib which can go further. We just want to keep things simple and hope to have the Gulp 4 release which will fix that.

### Watch with function

The most common use of the watch API is to list files and just indicate which tasks to launch on a change. To gain some performance we go further by using the function version which ables us to have a function called on every change. As we have an `event` object which describe the change, we can be more specific.

The use case is the need of the injection. Many changes will only be a change on an existing files. This needs to trigger the pre-processing but not the injection. On the oposite, when it's a file creation, we need to relaunch the injection which will trigger the pre-processing by dependency.

### What is watched

As you can imagine, there is one watch expression for each type of files which trigger the related task.

Two remarks could be made:
- Root HTML files and the `bower.json` are watched to trigger the injection in order to react on modification in the `index.html` or an modification of the list of the dependencies.
- All HTML modification trigger a Browser Sync, indeed, as Gulp is responsible to trigger Browser Sync reload, a template modification needs to trigger a reload even when there is no other processing to launch.


## `gulp/server.js`

The generator ship a fully featured development server through the use of [Browser Sync](http://www.browsersync.io/). Don't hesitate to look at its website to know more about all its features and options.

The `serve` task has as only goal to configure and launch it.

### Browser Sync configuration

The base directories for Browser Sync are `.tmp/serve` and `src` with a priority for `.tmp/serve`. The processed version of a file has to be chosen over the source one.

As the `bower_components` folder is not located in any of the base paths, a special routes is added for this folder to be addressed by `/bower_components`.

The default Browser Sync port is `3000`, if you ever need to change it, head over to the [gulp/server.js](https://github.com/Swiip/generator-gulp-angular/blob/master/app/templates/gulp/_server.js#L42) file and add the `port` attribute to the *server* variable.
Example below : 
```javascript
browserSync.instance = browserSync.init({
    startPath: '/',
    server: server,
    browser: browser,
    port: 4000 // Add this line to change the default port
  });
```

Last configuration, the `browser` option is used to open the default browser to the root page.

Head over to [Browser Sync list of options](http://www.browsersync.io/docs/options/) for the full list of available configurations for BrowserSync.

### Proxy

Browser Sync is powered by an express server. The API allows us to inject any Express middleware. Behind comments, an example of use of [http-proxy-middleware](https://github.com/chimurai/http-proxy-middleware) is prepared.

The middleware allows very simply to add a proxy which takes all requests to a specific context a redirect it to another server.

It allows to work very simply with a backend server without dealing with CORS configurations.


## `gulp/unit-test.js`

The `test` task is targeted to launch a fully configured Karma / Jasmine / PhantomJS configuration.

### Limits between Gulp / Karma

Inside the Gulp file, there is not much as the most part of the Karma configuration stays in the `karma.conf.js`. The Gulp file mainly launch Karma through its Node API (`gulp-karma` is deprecated in profit of the Node API).

Our objective are to allow user to use Karma without Gulp if needed. Most of the times to be plugged inside an IDE.

As we wanted to keep some useful tools from the generator. It's from the Karma configuration file that some tools or configuration of the generator which are called.

### `karma.conf.js`

The `listFiles` function at the start of the file use [wiredep](https://github.com/taptapship/wiredep) and the `gulp/conf.js` file to list the files of the project the same way the injection does. This way, the user should never has to change the file list in the Karma configuration.

Past that two Karma plugin are used:
- [angularFilesort](https://www.npmjs.com/package/karma-angular-filesort): to order script files like in the injection.
- [ngHtml2JsPreprocessor](https://github.com/karma-runner/karma-ng-html2js-preprocessor): to be able to load templates inside tests which is needed in directive tests especially.


## `gulp/e2e-tests.js`

The `protractor` task is build on top of the [gulp-protractor](https://github.com/mllrsohn/gulp-protractor) plugin which handles the downloading and the launching of an embedded Webdriver with Protractor.

With a dependency on the task `serve:e2e` which launch the server without opening a browser on it, the server is started and a dependency on the initialization of Webdriver, the protractor tests can be launched.

The `protractor.conf.js` are mainly default configurations.

## `gulp/build.js`

Inside this files, there is several Gulp tasks to organize the whole optimization process of the application.

The main goal is to create a `dist` folder fully portable which behave exactly like the source version.

### Main process

The main process is located in the `html` task. It contains the re-writing of the `index.html`, the concatenation and minifying of all files in one single Gulp stream.

As all files will be in the same stream, we use Gulp filters to filter a type of files to perform some transformation and remove the filter with the `restore()` method.

### Partials

One of the optimization is to mount all the partials or templates inside the script bundle in order to reduce the number of request at the loading. We do that in the `partials` task which use the [gulp-angularTemplatecache](https://www.npmjs.com/package/gulp-angular-templatecache) plugin in order to transform the HTML files in valid JavaScript Angular desclaration.

The Gulp stream load the HTML files from the sources, minify the code HTML, apply the AngularTemplateCache transformation and put them in a `.tmp/partials` to be injected in the main process with the same [gulp-inject](https://github.com/klei/gulp-inject) plugin already used.

### Useref

[gulp-useref](https://github.com/jonkemp/gulp-useref) is the backbone of the optimization process. Starting by the `index.html` it loads all the files using the `<!-- build:....` -> `<!-- endbuild -->` comments.

It adds all the files in the Gulp stream which ables us to filter them and apply transformations (line `.pipe(assets = $.useref.assets())`).

It also perform the concatenation and rewrite the `index.html` pointing on the new file (line `.pipe($.useref())`).

To understand where the files are located and how to call the targeted files, you have to look at the comments (not the Gulp file), basically, the syntax is: `<!-- build:{{type: css or js}}({{base path}}) {{target file path}} -->`.

More information on [gulp-useref](https://github.com/jonkemp/gulp-useref).

### Rev

Another great feature of the generator is to rename your optimized files with the hashcode of the content. It prevent all problems of client caches which prevent them to reload new version of the files. With the content hashcode, only the files which has changed will change names.

This feature is possible thanks to the [gulp-rev](https://github.com/sindresorhus/gulp-rev) which is used inside the main process. A second step [gulp-revReplace](https://github.com/jamesknelson/gulp-rev-replace) is needed for the files to be renamed inside the new `index.html` created by Useref.

### Images

Proposed as an advanced option, there is a task named `images` which can use [gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin) to optimize your images before putting them in the `dist` folder.

It has been removed by default and put behind an advanced option because the NPM dependency is heavy and the image optimization slow so finally lots of people didn't want it anymore.

### Fonts

Some Bower dependencies embed font files. To handle this particular case, there is `fonts` task which copies font files located by wiredep. This task only copy the in the `dist/font` directory.

As we can't keep the original relative path of the font with the CSS file which include it, there is the need of replacing the link. It's why you find with some options the use of [gulp-replace](https://github.com/lazd/gulp-replace) inside the main process. But this solution is **not generic** and could need to be duplicate with the use of others dependencies than default ones.

### Other

We don't know what files you'll have in the `src` folder. We only knows about some types we have specific rules to handle them.

The task `other` simply locate all the files which are not already processed in the `src` folder and copy at them at the same location in the `dist` folder in order to keep the same paths.
