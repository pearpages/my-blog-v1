---
layout: post
sidebar-align: left
title: "An Angular2 example"
date:   2016-04-30 20:12:35
categories: javascript angular angular2
author: Pere Pages
---

* TOC
{:toc}

## Component

```
Component = Template + Class + Metadata
```

## Application Arhictecture

- App Component
  - Product Data Service
  - Welcome Component
  - Product List Component
    - Star Component
  - Product Detail Component
    - Star Component

## Concepts

- Components
  - Nested Components
- Templates, Interpolation, and Directives
- Data Binding & Pipes
- Services and Dependency Injection
- Retrieving Data Using Http
- Navigation and Routing

## Javascript Language Specification

- ECMAScript (ES)
- ES 3
- ES 5
- ES 2015 (formerly known as ES6)
  - Must be transpiled

## Typescript

- Open soruce
- Superset of Javascript
- Transpiles to Javascript
- Strongly typed
  - Typescript type definition files (*.d.ts)
- Class-based object-orientation

## IDEs for Typescript

- Visual Studio
- Visual Studio Code
- WebStorm
- Atom
- Eclipse
- ...

## Setting up Our Environment

It is a bit laborious.

1. Create the *tsconfig.json* file
2. Create the *package.json* file
3. Create the *typings.json* file
4. Install the **libraries** and **typings**
5. Create the host Web page (*index.html*)
6. Create the *main.ts* file (*bootstrapper)*

## Modules

- Angular1 Modules
- Typescript Modules
- ES 2015 Modules
- Angular2 Uses ES 2015 Modules

### ES 2015 Modules

#### Export

```typescript
// product.ts

export class Product {
  
}
```

#### Import

```typescript
// product-list.ts

import {Product} from './product'
```

## Components

```
Component = Template + Class + Metadata
```

Once we give the *@Component* metadata we get a Component.

> Decorator: A function that adds *metadata* to a class, its members, or its method arguments.

```typescript
import {Component} from 'angular2/core';

@Component({
    selector: 'pm-app',
    template: `
    <div><h1>{{pageTitle}}</h1>
        <div>My First Component</div>
    </div>
    `
})
export class AppComponent {
    pageTitle: string = 'Product Management';
}
```

```typescript
// main.ts
import {bootstrap} from 'angular2/platform/browser';
import {AppComponent} from './app.component';

bootstrap(AppComponent);
```

```html
<!-- indexx.html -->

<!-- System.import('app/main'); -->

<body>
  <pm-app>Loading App ...</pm-app>
</body>
```

## Angular is Modular

- core
- animate
- http
- router

## Bootstrapping

```typescript
// main.ts
import {bootstrap} from 'angular2/platform/browser';
import {AppComponent} from './app.component';

bootstrap(AppComponent);
```

## Templates

- Inline Template
- Linked Template

```Typescript
template:
"<h1>{{pageTitle}}</h1>"
```

```Typescript
// ES 2015 back tick
template: `
<div>
  <h1>{{pageTitle}}</h1>
  <div>
    My First Component
  </div>
</div>
```

```typescript
  templateUrl: 'product-list.component.html'
```

## Include Component

```typescript
import {Component} from 'angular2/core';
// 1
import {ProductListComponent} from './products/product-list.component'

@Component({
    selector: 'pm-app',
    template: `
    <div><h1>{{pageTitle}}</h1>
        <pm-products></pm-products>
    </div>
    `,
    // 2
    directives: [ProductListComponent]
})
export class AppComponent {
    pageTitle: string = 'Product Management';
}
```

## Binding

> Coordinates communication between the component's class and its template and often involves passing data.

## Directive

> Custom HTML element or attribute used to power up and extend our HTML.

- Custom
- Built-in (*ngIf, *ngFor)

```typescript
<table *ngIf='products.length'>
  <thead></thead>
  <tbody></tbody>
</table>
```

```typescript
// the hash # makes the product variable a local variable of the loop
<tr *ngFor='#product of products'>
    <td></td>
    <td>{{product.productName}}</td>
    <td>{{product.productCode}}</td>
    <td>{{product.releaseDate}}</td>
    <td>{{product.price}}</td>
    <td>{{product.starRating}}</td>
</tr>
```

### for...of

- Iterates over iterable objects, such as an array.

### for...in

- Iterates over the properties of an object.

## Property Binding vs Interpolation

```html
<img [src]='product.imageUrl'>

<!-- Interpolation -->
<img src="{{product.imageUrl}}" >
<img src="http://openclipart.org/{{product.imageUrl}}">
```

```typescript
// ...
export class ProductListComponent {
    pageTitle: string = 'Product List';
    imageWidth: number = 50;
    imageMargin: number = 2;
// ...    
```

```html
<td><img [src]="product.imageUrl" [title]="product.productName" 
[style.width.px]='imageWidth' [style.margin.px]='imageMargin'></td>
```

## Event Binding

### Template

```html
<button (click)='toggleImage()' class="btn btn-primary">{{showImage ? 'Hide Images' : 'Show Images'}}</button>

<!-- ... -->

<!-- check the ngIf -->
<td><img *ngIf='showImage' [src]="product.imageUrl" [title]="product.productName" 
[style.width.px]='imageWidth' [style.margin.px]='imageMargin'></td>

<!-- ... -->
``` 

### Component

```typescript
// ...
export class ProductListComponent {
   // ...
    showImage: boolean = false;
   
    // ...
    toggleImage(): void {
        this.showImage = !this.showImage;
}
// ...
```

### Two-way Binding

#### Banana in a box

[()] <-- Means type and event binding at the same time.

```typescript
export class ProductListComponent {
  // ...
  listFilter: string = 'cart';
  // ...    
}
```

```html
<input type="text" [(ngModel)]='listFilter'>
```

## Pipes

> Transform bound properties before display.

- date
- number, decimal, percent, currency, ...
- json, slice
- custom

```html
<td>{{product.productName | uppercase}}</td>
<td>{{product.productCode | lowercase}}</td>
<td>{{product.releaseDate}}</td>
<td>{{product.price | currency:'EUR':true:'1.2-2'}}</td>
<td>{{product.starRating}}</td>
```

### Writing a custom Pipe

```typescript
@Pipe({
  name: 'productFilter'
})
export class ProductFilterPipe implements PipeTransform {
  
  transform(value: IProduct[], args: string[]): IProduct[] {}
}
```

```html
<!-- listFilter is the variable from the class that has two way data binding -->
<tr *ngFor = '#product of products | productFilter:listFilter'>
```

```typescript
import {PipeTransform,Pipe} from 'angular2/core';
import {IProduct} from './product';

@Pipe({
    name: 'productFilter'
})
export class ProductFilterPipe implements PipeTransform {

    transform(value: IProduct[], args: string[]): IProduct[] {
        let filter: string = args[0] ? args[0].toLocaleLowerCase() : null;
        
        // Array.filter() method
        return filter ? value.filter((product: IProduct) => 
            product.productName.toLocaleLowerCase().indexOf(filter) != -1): value;
    }    
}
```

## Interface

> A **specification** identifying a related set of properties and methods.

> A class commits to supporting the specification by **implementing** the interface.

> Use the interface as a **data type**.

```typescript
export interface IProduct {
  productId: number;
  productName: string;
  productCode: string;
  releaseDate: Date;
  price: number;
  description: string;
  starRating: number;
  imageUrl: string;
  calculateDiscount(percent: number): number;
}
```

```typescript
import { IProduct } from './product';

export class ProductListComponent {
  products: IProduct[] = [];
}
```

If we don't need any methods we don't have the need a creating a **class** and we use an **interface** instead.

## Encapsulating component Styles

```typescript
@Component({
    selector: 'pm-products',
    templateUrl: 'app/products/product-list.component.html',
    styleUrls: ['app/products/product-list.component.css']
})
```

## Component Lifecycle / Using a Lifecycle Hook

1. Create
2. Render
3. Create and render children
4. Process changes
5. Destroy

## OnInit

Perform component initialization, retrieve data.

## OnChanges

Perform action after change to input properties.

## OnDestroy

Perform cleanup.

```typescript
import { OnInit } from 'angular2/core';

export class ProductListComponent implements OnInit {
  // ...
  
  ngOnInit(): void {
    console.log('In OnInit');
  }
  
  // ...
}
```

## Nested Components

### Input Properties

- Attached to a property of any type
- Prefix with @; Suffix with ()

```typescript
@Input() rating: number;
```

```html
<ai-star [rating]='product.starRating'></ai-star>
```

### Output Event

- Attached to a property declared as an EventEmitter
- Use the generic argument to define the event payload type
- Use the new keyword to create an instance of the *EventEmitter*

```html
<div class="crop"
[style.width.px]="starWidth"
[title]="rating"
(click)='onClick()'>
```

```typescript
import {Component,OnChanges,Input,Output,EventEmitter} from 'angular2/core';

@Component({
    selector: 'ai-star',
    templateUrl: 'app/shared/star.component.html',
    styleUrls: ['app/shared/star.component.css']
})
export class StarComponent implements OnChanges {
    @Input() rating: number;
    starWidth: number;
    @Output() ratingClicked: EventEmitter<string> = new EventEmitter<string>();
    
    ngOnChanges(): void {
        this.starWidth = this.rating * 86 / 5;
    }
    onClick() {
        this.ratingClicked.emit(`The rating ${this.rating} was clicked!`);
    }
}
```

```html
<td>
    <ai-star [rating]='product.starRating' (ratingClicked)='onRatingClicked($event)'>
    </ai-star>
</td>
```

```typescript
onRatingClicked(message: string):void {
    this.pageTitle = 'Product List: ' + message;
}
```

## Services and Dependency Injection

> A Service is a class with a focused purpose.

Used for features that:

- Are independent from any particular component
- Provide shared data or logic across components
- Encapsulate external interactions

### Dependency Injection

> A coding patterin in which a class receives the instances of objects it needs (called dependencies) from an external source rather than creating them itself.

### Building a Service

1. Create the service class
2. Define the metadata with a decorator
3. Import what we need

### Register a service

1. Register a provider
  - Code that can create or return a service, typically te service class itself.
2. Define as part of the component metadata
3. Injectable to component AND any of its children

```typescript
import {Component} from 'angular2/core';
import {ProductListComponent} from './products/product-list.component'
import {ProductService} from './products/product.service';

@Component({
    selector: 'pm-app',
    template: `
    <div><h1>{{pageTitle}}</h1>
        <pm-products></pm-products>
    </div>
    `,
    directives: [ProductListComponent],
    providers: [ProductService]
})
export class AppComponent {
    pageTitle: string = 'Product Management';
}
```

```typescript
import { Injectable } from 'angular2/core';
import { IProduct } from './product';

@Injectable()
export class ProductService {
    
    getProducts(): IProduct[] {
        return [
          // ...
        ];
    }
}
```

```typescript
import {Component,OnInit} from 'angular2/core';
import {IProduct} from './product';
import {ProductFilterPipe} from './product-filter.pipe';
import {StarComponent} from '../shared/star.component';
import {ProductService} from './product.service';

@Component({
    selector: 'pm-products',
    templateUrl: 'app/products/product-list.component.html',
    styleUrls: ['app/products/product-list.component.css'],
    pipes: [ProductFilterPipe],
    directives: [StarComponent]
})
export class ProductListComponent implements OnInit{
    pageTitle: string = 'Product List';
    imageWidth: number = 50;
    imageMargin: number = 2;
    showImage: boolean = false;
    listFilter: string = null;
    products: IProduct[] = null;
    
    constructor(private _productService: ProductService) {
        
    }
    
    toggleImage(): void {
        this.showImage = !this.showImage;
    }
    
    ngOnInit(): void {
        this.products = this._productService.getProducts();
    }
    
    onRatingClicked(message: string):void {
        this.pageTitle = 'Product List: ' + message;
    }
}
```

## Retrieving Data Using Http

- Setting up
- Sending an Http Request
- Observables and Reactive Extensions
- Subscribing to an Observable

- An array whose items arrive asynchronously over time
- Helps manage asynchronous data
- Proposed feature for ES 2016
- Use Reactive Extensions (RxJS)
- Used within Angular

An Observable works like an Array, so we can use the *map* method. We use an arrow function.

[Explanation](http://rxmarbles.com)

### Promise vs Observable

|Promise|Observable|
|:--|:--|
|Returns a single value|Works with multiple values over time|
|Not cancellable|Cancellable|
||Supports map, filter, reduce and similar operators|

### Setting Up

- Include the Angular 2 Http script
- Register HTTP_PROVIDERS (at the appropiate level)
- Import RxJS

```html
<!-- HTTP -->
<script src="node_modules/angular2/bundles/http.dev.js"></script>
```

```typescript
// add the level required e.g.: app.component
import {HTTP_PROVIDERS} from 'angular2/http';
import 'rxjs/Rx'; // Load all features

@Component({
    // ...
    providers: [HTTP_PROVIDERS]
})
```

#### In the Service

- Import what we need
- Define a dependency for the http client service
  - Use a constructor parameter
- Create a method for each http request
- Call the desired http method, such as get
  - Pass in the Url
- Map the Http response to a JSON object
- Add error handling

#### In the Subscribing

- Call the subscribe method of the returned observable
- Provide a function to handle an emitted item
  - Normally assigns a property to the returned JSON object
- Provide an error function to handle any returned errors

### Sending an Http Request

```typescript
import {Http, Response} from 'angular2/http';
import {Observable} from 'rxjs/Observable'

@Injectable()
export class ProductService {
    private _productUrl = 'www.myWebService.com/api/products';
    constructor(private _http: Http) {}
    
    getProducts(): Observable<IProduct[]> {
        return this._http.get(this._productUrl)
            .map((response: Response => <IProuct[]>response.json()); 
    }
}
```

### Handling Errors

```typescript
getProduts(): Observable<IProduct[]> {
    return this._http.get(this._productUrl)
        .map((response: Response) => <IProduct[]>response.json())
        .do(data => console.log('All: ' + JSON.stringify(data)))
        .catch(this.handleError);
}

private handleError(error: Response) {}
```

### Subscribing to an Observable

```typescript
ngOnInit(): void {
    this._productService.getProducts()
        .subscribe(
            products => this.products = products,
            error => this.errorMessage = <any>error);
        );
}
```

## Navigation and Routing

- Configure a route for each component
- Define options/actions
- Tie a route to each option/action
- Activate the route based on user action
- Activating a route displays the component's view

### Setting Up

1. Include the Angular 2 router script
2. Define the base element
3. Register ROUTER_PROVIDERS

```html
<base href="/">
<!-- Required for routing -->
<script src="node_modules/angular2/bundles/router.dev.js"></script>
```

```typescript
import {ROUTER_PROVIDERS,RouteConfig} from 'angular2/router';

@Component({
    // ...
    providers: [ROUTER_PROVIDERS]
})
```

### Configuring Routes

- a route name
- a URL segment
- an associated component

The name must be in *PascalCase*.

```typescript
@RouteConfig([
    {path: '/welcome', name: 'Welcome', component: WelcomeComponent, useAsDefault: true},
    {path: '/products', name: 'Products', component: ProductListComponent}
])
```

### Trying Routes to Actions

- Menu option, link, image or button that activates a route
- Typing the Url in the address bar / bookmark
- The browser's forward or back buttons

```typescript
// ...
import {ROUTER_PROVIDERS,RouteConfig} from 'angular2/router';
import {WelcomeComponent} from './home/welcome.component';

@Component({
    selector: 'pm-app',
    template: `
    <ul class='nav navbar-nav'>
        <li><a>Home</a></li>
        <li><a>Product List</a></li>
    </ul>
    `,
    directives: [ProductListComponent],
    providers: [ProductHttpService,
    HTTP_PROVIDERS,
    ROUTER_PROVIDERS]
})
@RouteConfig([
    {path: '/welcome', name: 'Welcome', component: WelcomeComponent, useAsDefault: true},
    {path: '/products', name: 'Products', component: ProductListComponent}
])
// ...
```

### Placing the Views

```html
<router-outlet></router-outlet>
```

```typescript
import {Component} from 'angular2/core';
import {ProductListComponent} from './products/product-list.component'
import {ProductHttpService} from './products/product-http.service';
import {HTTP_PROVIDERS} from 'angular2/http';
import 'rxjs/Rx'; // Load all features
import {ROUTER_PROVIDERS,ROUTER_DIRECTIVES,RouteConfig} from 'angular2/router';
import {WelcomeComponent} from './home/welcome.component';

@Component({
    selector: 'pm-app',
    template: `
    <div>
        <nav class='navbar navbar-default'>
            <div class='container-fluid'>
                <a class='navbar-brand'>{{pageTitle}}</a>
                <ul class='nav navbar-nav'>
                    <li><a [routerLink]="['Welcome']">Home</a></li>
                    <li><a [routerLink]="['Products']">Product List</a></li>
                </ul>
            </div>
        </nav>
        <div class='container'>
            <router-outlet></router-outlet>
        </div>
    </div>
    `,
    directives: [ROUTER_DIRECTIVES],
    providers: [ProductHttpService,
    HTTP_PROVIDERS,
    ROUTER_PROVIDERS]
})
@RouteConfig([
    {path: '/welcome', name: 'Welcome', component: WelcomeComponent, useAsDefault: true},
    {path: '/products', name: 'Products', component: ProductListComponent}
])
export class AppComponent {
    pageTitle: string = 'Product Management';
}
```

### Passing Parameters to a Route

```typescript
// app.component
{path: '/product/:id', name: 'ProductDetail', component: ProductDetailComponent}
```

```typescript
// component with the link
import {ROUTER_DIRECTIVES} from 'angular2/router';

@Component({
    selector: 'pm-products',
    templateUrl: 'app/products/product-list.component.html',
    styleUrls: ['app/products/product-list.component.css'],
    pipes: [ProductFilterPipe],
    directives: [StarComponent,ROUTER_DIRECTIVES]
})
```

```html
<!-- link -->
<td>
    <a [routerLink]="['ProductDetail',{id: product.productId}]">
        {{product.productName}}
    </a>
</td>
```

```typescript
// some other component where we use the parameter
import {RouteParams} from 'angular2/router';

// ...
constructor(private _routeParams: RouteParams) {
    console.log(this._routeParams.get('id'));
}
```

Complete example in the Component that uses the url parameter

```typescript
import {Component} from 'angular2/core';
import {RouteParams} from 'angular2/router';

@Component({
    templateUrl: 'app/products/product-detail.component.html'
})
export class ProductDetailComponent {
    pageTitle: string = 'Product Detail';
    constructor(private _routeParams: RouteParams) {
        let id = +this._routeParams.get('id');
        this.pageTitle += `: ${id}`;
    }
}
```

### Activating a Route with Code

```typescript
import {Router} from 'angular2/router';

// ...

constructor(private _router: Router) {}

onBack(): void {
    this._router.navigate(['Products']);
}

// ...
```

## Angular2 Setup Revisited

### tsconfig.json

Typescript configuration file. Indicates that the folder where it is contained is the root folder.

```json
// these are needed so Angular2 can compile
"emitDecoratorMetadata": true,
"experimentalDecorators": true,
```

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false // if set to true we strongly type
  },
  "exclude": [
    "node_modules",
    // we ignore typings/main because these are for node
    // this also mean that we are compiling typings/browser
    "typings/main",
    "typings/main.d.ts"
  ]
}
```

### package.json

- scripts
- dependencies
- devDependencies

#### scripts

E.g.

```bash
npm start # doesn't need the run command
npm run tsc
npm run lite
npm run lite # lite-server is specifically written for Angular2
```

#### Dependencies

If we want to install only the *dependencies* and not the *devdependcies* we can use: ```npm install --production```.

### index.html

- router.dev.js
- http.dev.js
- system.src.js
- Rx.js
- angular2.dev.js

#### Polyfills

We add ES5 code so we can support the ES2015 syntax.

> In web development, a polyfill (or polyfiller) is additional code which provides facilities that are not built into a web browser. It implements technology that a developer expects the browser to provide natively, providing a more uniform API landscape.

#### Shim

It lets us use an API to an older environment.

> In computer programming, a shim is a small library that transparently intercepts API calls and changes the arguments passed, handles the operation itself, or redirects the operation elsewhere.

## More

- Material Design
- Angular Universal
- Web Workers
- Ionic
- Nativescript