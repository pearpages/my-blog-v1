
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