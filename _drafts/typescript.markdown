
[http://www.typescriptlang.org](http://www.typescriptlang.org)

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