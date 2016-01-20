
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