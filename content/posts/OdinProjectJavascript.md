+++
title = 'Odin Project Javascript'
date = 2024-01-31T18:28:57Z
draft = false
tags = 'study'
+++
## Factory Functions
One of the main problems with object constructors is that they look like regular JS functions, however operate very differently
These functions are very similar to object constructors work, but instead of using the new keyword to create an object, they set up and return the object within the function
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

// here is how you would assign multiple values with it
const nowFancyObject = { name, age, color };

```
