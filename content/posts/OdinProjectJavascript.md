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



### classes
Classes in javascript don't function in the same way as other OOP languages, in javascript they function pretty much the same as object constructors.





### getters and setters
getters and setters are used for simpler syntax, better data quality, and it's useful for behind-the-scenes

get and set are special functions triggered when a object property is read/set

There are two types of object properties, data properties and accessor properties


```Javascript
get let obj = {
  get propName() {
    // getter, the code executed on getting obj.propName
  },

  set propName(value) {
    // setter, the code executed on setting obj.propName = value
  }
};
```

The getter works when obj.propName is read, the setter when it is assigned.

For instance, if we have a user.object with **name** and **surname**
```Javascript
let user = {
  let user = {
  name: "John",
  surname: "Smith",

  get fullName() {
    return `${this.name} ${this.surname}`;
    // get here is used to give the object a function that it can display the outcome from
  }
  }
};

alert(user.fullName); // John Smith
```
- Now if you try and assign a value to user.fullname it will give an error

```Javascript 
let user = {
  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
    // the set is only activated when the user.fullName is **set**, so alert(user.fullName) would not work 
  }
};

// set fullName is executed with the given value.
user.fullName = "Alice Cooper";

alert(user.name); // Alice
alert(user.surname); // Cooper
```

### Accessor descriptors 
Descriptors for accessor properties are different from those for data properties.
For accessor properties there is no value or writable.

- accessor descriptors are get, set, enumerable and configurable 
```Javascript
let user = {
  name: "John",
  surname: "Smith"
};

Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
});

alert(user.fullName); // John Smith

for(let key in user) alert(key); // name, surname
```

## Modern Javascript
In 2010, several competing Js package manager emerged to help automating the process of downloading libraries from a central repo. Npm and yarn are the two most popular today.
- By using npm init you can create a package.json file, this is a conf file that npm uses to save all project info like dependencies

In 2009, a project named commonJS was started with the goal of specifying an ecosystem for js outside the browser. A big part of CommonJS was its specification for modules, which would finally allow js to omport and export code across files like other langs, without resorting to global variables. 

Node uses commonJS modules, you would write:
var moment = require("moment);
to load the moment module using node

Now this works for node, however if you tried to use it in browser, you'd get an error saying require is not defined because the browser does not have access to your filesystem. This means that loading modules has to be done dynamically.
This is where a module bundler helps, which finds all the require statements and replaces them with the actual cotent of the required file, and bundles them together into one file.
- The most popular bundlers are browserify and webpack

Transpiling code means converting the code in one lang to another similar lang, like from Typescript to Javascript 

A Task Runner is a tool that automates different parts of the build process, such as minifying code, running tests.
- Npm and Grunt are the most popular

- As project complexity grows, so do the benefits of well structured code.
- So it is good to break down code into smaller files/modules

#### webpack
If you give webpack a file as an entry point, it will build a dependancy graph based on all the imports/exports (which is just a tree of all the files/modules being imported)

If you are dealing with just bundling js then this is easy, but if your project includes css or assets then you will need to import your css file directly into your javascript. When webpack bundles your files it will try copy them into dist.

Since these files are not Javascript, webpack will not know how to process them unless you tell it how to by including the correct loaders and rules. 

Since we would like to keep all our dev work within src and leave dist for the build, we can use a plugin called html-webpack-plugin which will automatically build a html file in dist for us when we build project. It will also then auto add certain things to the html like our output bundle in a script tag.

By default, it will use a blank template, so the resulting html file will essentially be the usual boilerplate with our script. If you make a dist/index.html then it would be overwritten, we can also tell it to use a template and put a path to our own html file that is in src.js
