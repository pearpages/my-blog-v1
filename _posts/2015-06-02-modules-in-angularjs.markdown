---
layout: post
sidebar-align: left
title: "Modules in AngularJS"
date:   2015-06-02 08:33:15
categories: javascript angularjs
---
#### Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Modules in Javascript (in General)

#### Links

**Stackoverflow** [What is the difference between browserify/requirejs modules and ES6 modules](http://stackoverflow.com/questions/28674652/what-is-the-difference-between-browserify-requirejs-modules-and-es6-modules)

**@Andy** for the blog by *Addy Osmani*. [Writing Modular JavaScript With AMD, CommonJS & ES Harmony](http://addyosmani.com/writing-modular-js/)

### Script Loading

At present, script loading is a means to a goal, that goal being modular JavaScript that can be used in applications today - for this, use of a compatible script loader is unfortunately necessary.

#### AMD

AMD adopts a browser-first approach to development, opting for asynchronous behaviour and simplified backwards compatability but it doesn't have any concept of File I/O. It supports objects, functions, constructors, strings, JSON and many other types of modules, running natively in the browser. It's incredibly flexible.

#### CommonJS

CommonJS on the other hand takes a server-first approach, assuming synchronous behaviour, no global *baggage* as John Hann would refer to it as and it attempts to cater for the future (on the server). What we mean by this is that because CJS supports unwrapped modules, it can feel a little more close to the ES.next/Harmony specifications, freeing you of the define() wrapper that AMD enforces. CJS modules however only support objects as modules.

## In AngularJS

**Stackoverflow** [Check this link to follow the debate](http://stackoverflow.com/questions/14621581/angular-best-practice-to-structure-modules)

Folders-by-Feature Structure: Create folders named for the feature they represent. When a folder grows to contain more than 7 files, start to consider creating a folder for them. Your threshold may be different, so adjust as needed.

#### Links

**@john_papa** [John Pappa's AngularJS Style Guide](https://github.com/johnpapa/angular-styleguide).

**Cliff Meyers**: [Code Organization in Large AngularJS and JavaScript Applications](http://cliffmeyers.com/blog/2013/4/21/code-organization-angularjs-javascript)

### Tips for Common Code

Every application has common code that is used by many modules. We just need a place for it which can be a folder named "common" or "shared" or whatever you like. In really big applications there tends to be a lot of overlap of functionality and cross-cutting concerns. This can be made manageable through a few techniques:

* If your module's objects require direct access to several "common" objects, write one or more Facades for them. This can help reduce the number of collaborators for each object since having too many collaborators is typically a code smell.
* If your "common" module becomes large subdivide it into submodules that address a particular functional area or concern. Ensure your application modules use only the "common" modules they need. This is a variant of the "Interface segregation principle" from SOLID.
* Add utility methods onto $rootScope so they can be used by child scopes. This can help prevent having to wire the same dependency (such as "PermissionsModel") into every controller in the application. Note that this should be done sparingly to avoid cluttering up the global scope and making dependencies non-obvious.
* Use events to decouple two components that don't require an explicit reference to one another. AngularJS makes this possible via the $emit, $broadcast and $on methods on the Scope object. A controller can fire an event to perform some action and then receive a notification that the action completed.


### Quick Note on Assets and Tests

I think there's more room for flexibility with respect to organizing HTML, CSS and images. Placing them in an **assets** subfolder of the module probably strikes the best balance between encapsulating the module's asset dependencies and not cluttering things up too much. However I think a separate top-level folder for this content which contains a folder structure that **mirrors** the app's package structure is reasonable too. I think it works well for tests as well.

### Big Project Structure

```bash
/app
  /img         # application-level images
  /css         # application-level css styles
  /js          # application-level javascripts
  /modules             # application modules
          /gallery               # independent module with its own infrastructure
                 /controllers    # gallery module's controllers
                 /css            # gallery module's css styles
                 /directives     # gallery module's directives
                 /img            # gallery module's images
                 /filters        # gallery module's filters
                 /services       # gallery module's services
                 /views          # gallery module's views (htmls)
                 / ...           # other gallery module component folders
                 galleryMod.js   # the module itself

          /user                  # independent module with its own infrastructure
                 /controllers    # user module's controllers
                 / ...           # other user module component folders
                 userMod.js      # the module itself

          / ...                  # other modules

  / ...                # other application-level folders
  index.html
```

### Alternative enterprise project organization (simplified)

```bash
/app
  /img         # application-level images
  /css         # application-level css styles
  /js          # application-level javascripts
  /modules             # application modules
          /gallery               # independent module with its own infrastructure
                 /js             # gallery module's javascripts (includes 
                                 # services.js, directives.js, filters.js, ...)
                 /css            # gallery module's css styles
                 /img            # gallery module's images
                 /views          # gallery module's views (htmls, "partials")
                 / ...           # other gallery module component folders
                 galleryMod.js   # the module itself

          /user                  # independent module with its own infrastructure
                 /controllers    # user module's controllers
                 / ...           # other user module component folders
                 userMod.js      # the module itself

          / ...                  # other modules

  / ...                # other application-level folders
  index.html
```

### Middle project organization (without modules)

```bash
/app
  /img            # application's images
  /css            # application's css styles
  /controllers    # application's controllers
  /directives     # application's directives
  /filters        # application's filters
  /services       # application's services
  /views          # application's views (htmls)
  / ...           # other component folders
  index.html
```

### Simple project organization (just like a seed)

```bash
/app
  /img            # application's images
  /css            # application's css styles
  /js             # application's javascripts (includes 
                  # services.js, directives.js, filters.js, ...)
  /views          # application's views (htmls), e.g. partials
  / ...           # other component folders
  index.html
```