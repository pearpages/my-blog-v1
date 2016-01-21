
[Typescript: http://www.typescriptlang.org](http://www.typescriptlang.org)

## Why?

The main feature of Typescript is that makes the code, above all, more maintainable.

## What is Typescript?

> "TypeScript is a typed superset of Javascript that compiles to plain Javascript"

### Flexible options

- Any Browser
- Any Host
- Any OS
- Open Source
- Tool Support (Sublime)

### Key TypeScript Features

- Supports standard Javascript code
- Provides static typing
- Encapsulation through classes and modules
- Support for constructors, properties, functions
- Define interfaces
- function support (lambdas)
- Intellisense and syntax checking

### Typescript Features

```
tsc first.ts
```

TypeScript

```typescript
class Greeter {
    greeting: string;
    construct (message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}
```

Translation to Javascript

```javascript
var Greeter = (function (){
    function Greeter(message) {
        this.greeting = message;
    }
    Greeter.prototype.greet = function () {
        return "Hello, " + this.greeting;
    }
    return Greeter;
    })();
```

## Syntax, Keywords and Code Hierarchy

|Keyword|Description|
|:---|:---|
|**class**|Container for members such as properties and functions|
|**constructor**|Provides initialization functionality in a class|
|**exports**|Export a member from a module|
|**extends**|Extend a class or interface|
|**implements**|Implement an interface|
|**imports**|Import a module|
|**interface**|Defines a code contract that can be implemented by types|
|**module**|Container for classes and other code|
|**public/private**|Member visibility modifiers|
|**...**|Rest parameter syntax|
|**=>**|Arrow syntax used with definitions and functions|
|**<typeName>**|<> characters use to cast/convert between types|
|**:**|Separator between variable/parameter names and types|

### Hierarchy

```
Module
Class --> Interface
Fields, Constructor, Properties, Functions

```

### Tool / Framework Support

```
Node.js
Sublime
Emacs
Vi
Visual Studio
TypeScript Playground // a web page
```

Building the ts to js in Sublime

```
Tools > Build System > New Build System
```

Code example

```
class Car {
    engine: string;
    constructor(engine: string) {
        this.engine = engine;
    }

    start() {
        alert('Engine started: ' + this.engine);
    }

    stop() {
        alert('Engine stopped: ' + this.engine);
    }
}

window.onload = function () {
    var car = new Car('V8');
    car.start();
    car.stop();
}
```

## Typing, Variables and Functions

### Grammar, Declarations, and Annotations

```typescript
var an1; // any type
var num1: number; // type annotation
var num2: number  = 2; // type annotation
var num3 = 3; // type inference
var num4 = num3 + 100; // type inference
var str1 = num1 + 'some string'; // Error!
```

```typescript
init : (s: string, p: string, c: string) => void = function (startButton, pauseButton, clearButton) {
    //...
};
```

### Ambient Declarations

```typescript
declare var document;
```

```typescript
/// <reference path="jquery.d.ts" />
declare var $;
```

```typescript
/// <reference path="typings/knockout-2.2.d.ts />"
declare var ko;

module whatever {
    var name = ko.observable('John Papa');
    var id = ko.observable(1);
}
```

### Any and Primitive Types

+ any
+ number
+ boolean
+ string
+ array
+ indexer
+ null
+ undefined

### Object Types

+ functions
+ class
+ module
+ interface
+ literal types

```typescript
// ? means optional
var squereIt = function (rect: {
    h: number;
    w?: number;
    }) {
        if(rect.w === undefined) {
            return rect.h * rect.h;
        }
        return rect.h * rect.w;
    };
```

### Functions 

```typescript
var myFunc = function (h: number, w: number) {
    return h * w;
}
```

```typescript
var myFunc = (h: number, w: number) => h * w;
```

```typescript
var greetMe: (msg: string) => void;
```

```typescript
module utilities {
    var squareItSimple = (h: number,w: number) => h * w;
}
```

```typescript
var helloWorld: (name?: string) => void;
```

```typescript
module utilities{
    var squareIt: (rect: {h: number; w?: number;}) => number;

    squareIt = function(rect) {
        if (rect.w !== undefined) {
            return rect.h * rect.w;
        }
        return rect.h * rect.h;
    };

    var rectA = {h: 7};
    var rectB = {h: 7, w: 12};

    console.log(squareIt(rectA));
    console.log(squareIt(rectB));
}
```

### Interfaces

```typescript
module utilities {
    
    interface SquareFunction {
        (x: number): number;
    }

    var squareItBasic : SquareFunction = (num: number) => num * num;

    interface Rectangle {
        h: number;
        w? : number;
    }

    var squareIt: (rect: Rectangle) => number;

    squareIt = function(rect) {
        if (rect.w !== undefined) {
            return rect.h * rect.w;
        }
        return rect.h * rect.h;
    };

    var rectA = {h: 7};
    var rectB = {h: 7, w: 12};

    console.log(squareIt(rectA));
    console.log(squareIt(rectB));
}
```

```typescript
module people {
    
    interface Person {
        name: string;
        age?: number;
        kids: number;
        calcPets: () => number;
        makeYounger: (years: number) => void;
        greet: (msg: string) => string;
    }

    var p: Person = {
        favoriteMovie: 'LOTR', // this still works if the interface is defined
        name: 'Colleen',
        age: 40,
        kids: 4,
        calcPets: function () {
            return this.kids * 2;
        },
        makeYounger: function (years: number) {
            this.age -= years;
        },
        greet: function (msg: string) {
            return msg + ', ' + this.name;
        }
    };

    var pets = p.calcPets();
    console.log(pets);

    p.makeYounger(15);
    var newAge = p.age;
    console.log(newAge);

    var msg = p.greet('Good day to you');
    console.log(msg);
}
```

```typescript
module ratings {
    interface ratesEval {
        addRating(rating: number) => void;
        calcRating: () => number;
    }

    function myFunction(): ratesEval {
         function addRating (rating) {
            // ...
         }

         function calcRating () {
            // ...
            return 3;
         }

         return {
            addRating: addRating,
            calcRating: calcRating
         }
    }

    var rates = myFunction();
    rates.addRating(4);
    rates.addRating(5);
    rates.addRating(5);
    console.log(s.calcRating());
}
```

### Ambient Declarations for external references

files ```*.d.ts```

## Classes and Interfaces

### Defining Classes

Classes in Javascript are just **containters** to encapsulate functionality.

- Fields
- Constructors
- Properties
- Functions

#### Properties

Properties act as filters and can have get or set blocks.

Propertes are only available when compiling to ES5: tsc.exe --target ES5 YourFile.ts

```typescript
class Car {
    constructor(public engine: string) {}
}
```

```typescript
class Car {
    // Fields
    engine: string;

    // Properties
    private _engine: string;

    // Constructor
    constructor(engine: string) {
        this.engine = engine;
    }

    // Functions
    start() {
        return "Started " + this.engine;
    }

    stop() {
        return "Stopped " + this.engine;
    }

    get engine(): string {
        return this._engine;
    }

    set engine(value: string) {
        if (value == undefined) throw 'Supply an Egine!';
        this._engine = value;
    }
}
```

### Complex Types

```typescript
class Engine {
    constructor(public horsePower: number, public engineType: string) {}
}

class Car {
    private _engine: Engine;

    constructor(engine: Engine) {
        this.engine = engine; // complex type
    }

    get engine(): string {
        return this._engine;
    }

    set engine(value: string) {
        if (value == undefined) throw 'Supply an Engine!';
        this._engine = value;
    }
}

var engine = new Engine(300, 'V8');
var car = new Car(engine);
```

### Defining Classes

```typescript
class Engine {
    constructor(public horsePower: number,public engineType: string) {}
}

class Car {
    private _engine: Engine;

    constructor(engine: Engine) {
        this.engine = engine;   
    }

    get engine(): Engine {
        return this._engine;
    }

    set engine(value: Engine) {
        if (value == undefined) throw 'Plase supply an engine';
        this._engine = value;
    }

    start() : void{
        console.log('Car engine started ' + this._engine.engineType);
    }
}

var engine = new Engine(300,'V8');
var car = new Car(engine);
console.log(car.engine.engineType);
car.start();
```

### Property Limitations

Propertes are only available when compiling to ES5: ```tsc.exe --target ES5 YourFile.ts```

## Casting Types and Definition Files

### Casting

```typescript
var table: HTMLTableElement = 
<HTMLTableElement>document.createElement('table');
```

### Type Definition Files

*lib.d.ts* file is built-in out of the box for the DOM and JavaScript

[https://github.com/borisyankov/DefintelyType](https://github.com/borisyankov/DefintelyType)

## Extending Types

```typescript
class ChildClass extends ParentClass {
    constructor() {
        super(); // the base class constructor
    }
}
```

```typescript
class Auto {
    engine: Engine;
    constructor(engine: Engine) {
        this.engine = engine;
    }
}

class Truck extends Auto {
    fourByFour: bool;
    constructor(engine: Engine, fourByFour: bool) {
        super(engine);

        this.fourByFour = fourByFour;
    }
}
```

### Example

```typescript
class Engine {
    constructor(public horsePower: number, public engineType: string) {}

    start(callback: (startStatus: bool, engineType: string) => void) {
        window.setTimeout( () => {
            callback(true,this.engineType);
            }, 1000);
    }

    stop(callback: (stopStatus: bool, engineType: string) => void) {
        window.setTimeout( () => {
            callback(true, this.engineType);
            }, 1000);
    }
}

class Accessory {
    constructor(public accessoryNumber: number, public title: string) {}
}

class Auto {
    private _basePrice: number;
    private _engine: Engine;
    make: String;
    model: String;
    accessoryList: string;

    constructor(basePrice: number, engine: Engine, make: string, model: string) {
        this.engine = engine;
        this.basePrice = basePrice;
        this.make = make;
        this.model = model;
    }

    calculateTotal(): number {
        var taxRate = .08;
        return this.basePrice + (taxRate * this.basePrice);
    }

    // addAccessories(new Accessory(), new Accessory())
    addAccessories(...accessories: Accessory[]) {
        this.accessoryList = '';
        for(var i = 0; i < accessories.length; i++) {
            var ac = accessories[i];
            this.accessoryList += ac.accessoryNumber + ' ' + ac.title + '<br/>';
        }
    }

    // ...

}

class Truck extends Auto {
    bedLength: string;
    fourByFour: bool;

    constructor(basePrice: number, engine: Engine, make: string, model: string, bedLength: string, fourByFour: bool) {
        super(basePrice, engine, make, model);
        this.bedLength = bedLength;
        this.fourByFour = fourByfour;
    }
}
```

## Using Interfaces

Interfaces provide a way to enforce a "contract".

```typescript
interface IEngine {
    start(callback: (startStatus: bool, engineType: string) => void): void;
    stop(callback: (stopStatus: bool, engineType: string) => void): void;
}

interface IAutoOptions {
    engine: IEngine;
    basePrice: number;
    state: string;
    make?: string;
    model?: string;
    year?: string;
}

class Engine implements IEngine {
    constructor(public horsePower: number, public engineType: string) {}

    start(callback: (startStatus: bool, engineType: string) => void) { 
        window.setTiemout(() => {callback(true, this.engineType);
            }, 1000);
    }

    stop(callback: (callback: (stopStatus: bool, engineType: string) => void) {
        window.setTimeout(() => {callback(true, this.engineType);
            },1000);
    }
}
``` 

### Using Interface as a Type

```typescript
class Auto {
    engine: IEngine; // interface as a type
    basePrice: number;
    // ...

    constructor(data: IAutoOptions) {
        this.engine = data.engine;
        this.basePrice = data.basePrice;
    }
}
```

### Casting Interfaces

```typescript
var myEngine = <Engine>auto.engine;
console.log(myEngine.horsePower.toString());
```

### Extending and Interface

```typescript
interface IAutoOptions {
    engine: IEngine;
    basePrice: number;
    state: string;
    make?: string;
    model?: string;
    year?: number;
}

interface ITruckOptions extends IAutoOptions {
    bedLength?: string;
    fourByFour: bool;
}
```

#### Using and Extended Interface

```typescript
class Truck extends Auto {
    private _bedLength: string;
    fourByFour: bool;

    constructor(data: ITruckOptions) {
        super(data);
        this.bedLength = data.bedLength;
        this.fourByFour = data.fourByFour;
    }
}
```

Interfaces are also very useful to use for parameter objects.

```typescript
interface IAutoOptions {
    basePrice: number;
    engine: IEngine;
    state: string;
    make: string;
    model: string;
    year: number;
}

class Whatever {

    // ...

    constructor(options: IAutoOptions) {
        this.engine = options.engine;
        this.basePrice = options.basePrice;
        this.state = options.state;
        this.make = options.make;
        this.model = options.model;
        this.year = options.year;
    }
}
```

```typescript
interface ITruckOptions extends IAutoOptions {
    bedLength: string;
    fourByFour: bool;   
}

class Truck extends Auto {
    bedLength: string;
    fourByFour: bool;

    constructor(options: ITruckOptions) {
        super(options);
        this.bedLength = options.bedLength;
        this.fourByFour = options.fourByFour;
    }
}
```

## Modules 

If we define the same module in different files, they both will share the information contained inside them. But anything outside the module definition won't.

```typescript
module dataserveice {
    // code  
};
```

### Exporting Internal Modules

Check the *Module Pattern* and *Revealing Module Pattern*

```typescript
module Shapes{
    export class Rectangle {
        constructor(public height: number, public width: number) {
            // ...
        }
    }
}

var myRectangle = new Shapes.Rectangle(2,4); // Rectangle it is accessible because of the 'export' keyword

module Shapes { //extending shapes module defined above
    export class Circle {
        constructor (public radius: number) {
            // ...
        }
    }
}

var circle = new Shapes.Circle(20); // The same 
```

