In Node.js, some of the principles applied come directly from its creator, **Ryan Dahl**, from all the people who contributed to the core, from charismatic  gures in the community, and some of the principles are inherited from the **JavaScript** culture or are in uenced by the **Unix** philosophy.

In Node.js, a very common pattern for de ning modules is to expose only one piece of functionality, such as a function or a constructor, while letting more advanced aspects or secondary features become properties of the exported function or constructor.

## The Reactor Pattern

Pattern (reactor): handles I/O by blocking until new events are available from a set of observed resources, and then reacting by dispatching each event to an associated handler.

## libuv

[http://nikhilm.github.io/uvbook/](http://nikhilm.github.io/uvbook/)

Node.js core team created a C library called libuv, with the objective to make Node.js compatible with all the major platforms and normalize the non-blocking behavior of the different types of resource; libuv today represents the low-level I/O engine of Node.js.

node-core
bindings
V8 - libuv