In Node.js, some of the principles applied come directly from its creator, **Ryan Dahl**, from all the people who contributed to the core, from charismatic  gures in the community, and some of the principles are inherited from the **JavaScript** culture or are in uenced by the **Unix** philosophy.

In Node.js, a very common pattern for de ning modules is to expose only one piece of functionality, such as a function or a constructor, while letting more advanced aspects or secondary features become properties of the exported function or constructor.

## The Reactor Pattern

Pattern (reactor): handles I/O by blocking until new events are available from a set of observed resources, and then reacting by dispatching each event to an associated handler.

## libuv

[http://nikhilm.github.io/uvbook/](http://nikhilm.github.io/uvbook/)

Node.js core team created a C library called libuv, with the objective to make Node.js compatible with all the major platforms and normalize the non-blocking behavior of the different types of resource; libuv today represents the low-level I/O engine of Node.js.

```
node-core
bindings
V8 - libuv
```

## Zalgo

[http://blog.izs.me/post/59142742143/designing-apis-for-asynchrony](http://blog.izs.me/post/59142742143/designing-apis-for-asynchrony)

>If you have an API which takes a callback, and sometimes that callback is called immediately, and other times that callback is called at some point in the future, then you will render any code using this API impossible to reason about, and cause the release of Zalgo.

The lesson to learn from the unleashing Zalgo example is that it is imperative for an API to clearly de ne its nature, either synchronous or asynchronous.

## Revealing module pattern

```javascript
var module = (function() {
     var privateFoo = function() {...};
     var privateVar = [];
     var export = {
       publicFoo: function() {...},
       publicBar: function() {...}
    };
     return export;
})();
```

## Applying the callback discipline

```javascript
if (err) {
    return callback(err);
}
```

## Unlimited parallel execution

```javascript
var tasks = [...];
   var completed = 0;
   tasks.forEach(function(task) {
     task(function() {
       if(++completed === tasks.length) {
            finish(); 
        }
    });
});
function finish() {
  //all the tasks completed
}
```

## Limited parallel execution

```javascript
var tasks = [...];
   var concurrency = 2, running = 0, completed = 0, index = 0;
   function next() {              //[1]
     while(running < concurrency && index < tasks.length) {
       task = tasks[index++];
       task(function() {            //[2]
         if(completed === tasks.length) {
           return finish();
         }
         completed++, running--;
         next();
});
running++; }
} next();
   function finish() {
     //all tasks finished
}
```

## Promise

Promises are an abstraction that allow an asynchronous function to return an object called a promise, which represents the eventual result of the operation.

Promises states:

- Pending
- Settled
    - Fulfilled
    - Rejected


