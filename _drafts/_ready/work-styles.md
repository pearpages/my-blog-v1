# Styles

## General coding style

We basically stick to **Airbnb's** JavaSCript Coding Style guide which has kind of become an industry standard.

* [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)

## Angular-related coding style

We stick to the official Angular coding style-guide (shameless self-promotion: I contributed to this project back in the day and getting the community agreeing on that became a pain eventually, so for what it's worth let's leverage all that hard work pulled in). This should not be an issue should you have used the Angular-CLI in the past, but we currently do not use that tool ourselves but create items by hand instead, so being familiar with the naming conventions for code entities and classes is a must.

* [https://angular.io/guide/styleguide](https://angular.io/guide/styleguide)

## Projects Architecture

We pretty much embrace the guidelines issued by the Angular team in regards of application design, plus some nuances that are specific to Redux-driven projects with support for side effect model patterns (this is, the Effects lib).

* [https://angular.io/guide/architecture](https://angular.io/guide/architecture)
* [https://angular.io/guide/ngmodule](https://angular.io/guide/ngmodule)
* [https://github.com/ngrx/effects](https://github.com/ngrx/effects)
* [https://github.com/ngrx/example-app](https://github.com/ngrx/example-app)

Combining observables in a single stream is a common operation in our daily practice, so taking a look into operators such as

+ combineLatest()
+ concat()
+ switchMap()
+ flatMap()

> Warning: Please note that we're still on @ngrx/store v2.2.2. Eventually we will migrate to the @ngrx/platform (v4) project, which bundles the store, effects and some other utility libraries in a single npm package, but for the time being we will stick to the previous implementation until we allocate the time required to undertake the upgrade.

### Optimising data subscriptions and async bindings

Netanel Basal posts

* [https://netbasal.com/](https://netbasal.com/)

## IDE

My IDE of choice is Visual Code, and I pretty much use the same plugins as you. The msot important part is to ensure you have a proper ES6/TypeScript linter that can parse our current tslint.json spec.
