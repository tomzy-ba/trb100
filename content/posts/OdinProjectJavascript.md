+++
title = 'Odin Project Javascript'
date = 2024-01-31T18:28:57Z
draft = false
tags = 'study'
+++
## Factory Functions
One of the main problems with object constructors is that they look like regular JS functions, however operate very differently
These functions are very similar to object constructors work, but instead of using the "new" keyword to create an object, they set up and return the object within the function


They do not use the prototype, so they aren't as efficient


```Javascript
const User = function (name) {
  this.name = name;
  this.discordName = "@" + name;
}
// hey, this is a constructor - 
// then this can be refactored into a factory!

function createUser (name) {
  const discordName = "@" + name;
  return { name, discordName };
}
// and that's very similar, except since it's just a function,
// we don't need a new keyword

// here is a shorthand way to make an object
const thatObject = {name, age, color}

```
### The Module Pattern
Sometimes, you don't need a factory to make multiple objects - Instead, you can wrap sections of code together, hiding the variables and functions that you do not need. This can be done by wrapping your factory function in parentheses and immediately invoking it. This immediate function is called an Immediately Invoked Function Expression (IIFE) in short. This pattern of wrapping a factory function inside an IIFE is called the **Module Pattern** 

``` javascript
const calculator = (function () {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  return { add, sub, mul, div };
})();

calculator.add(3,5); // 8
calculator.sub(6,2); // 4
calculator.mul(14,5534); // 77476
```

In this example, we have a factory function creating some basic operations that we need only once. We can wrap it in parentheses and activate it using () returning the object stored in calculator
Think of these as mini-functions

The Module Pattern is used for **encapsulation**, the idea of building code/data singular units, with selective access. This is used for **Namespacing** (a technique that is used to avoid naming collisions)
The example code demonstrates this perfectly, the "add" variable is a common name so it's best to nest it inside of the Module Pattern
