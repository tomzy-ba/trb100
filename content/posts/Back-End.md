+++
title = 'Back End'
date = 2024-02-28T22:02:04Z
draft = false
tags = 'notes'
+++

### Intro
The front-end is where browser-side code is ran, stuff like markup, styling and scripting.
The back-end is **server-side** code, which is for storing data and serving the front end files to the browser.



### Express
#### Middleware
Middleware is just a javascript function that Express will call for you between the time it recieves a network request and the time it sends a response.
You can use these functions to: print details of the req to the console or check if the user has permissions to get the data they are requesting.

This is how a basic middleware function looks:

```javascript
const myLogger = function(req, res, next) {
  console.log("Request IP: " + req.ip);
  console.log("Request Method: " + req.method);
  console.log("Request date: " + new Date());

  next(); // THIS IS IMPORTANT!
}

app.use(myLogger)
``````



#### CRUD
CRUD stands for **Create, Read, Update, and Delete**. These are the four basic functions important for database driven apps.

These CRUD operations are slightly similar to the HTTP methods **POST, GET, PUT, and DELETE**

#### MVC
MVC stands for **Model, View, Controller** and refers to the structure of your code.

Models are the basic building blocks of a database, they encapsulate different types of data.
Views are the user interface components, such as screens, buttons, forms.
Controllers are the components that decide what view to display and what information goes in.

### Databases

Database API's are asynchronous, which means methods return immediate promises and other code can be executed in the meantime.
#### Models
A database model defines how your data is structured, organized, and used within a database. 
When designing your models it is good practice to have seperate models for each "object".

### Mongoose
*It is recommended to create a schema in it's own seperate file*
Mongoose models are created using the **Schema** object, Schema is like an object constructor for a database, it defines all the data types you can enter and what you can input in them. For Example:

```Javascript
const Schema = mongoose.Schema;

const SomeModelSchema = new Schema({
	name: String, //
	age: Number, //
	alive: Boolean, // these are called fields
	array: [],
});

// Compile model from schema
const SomeModel = mongoose.model("SomeModel", SomeModelSchema);
```

Mongoose also has built-in validators, they allow you to set the acceptable range of values and the error message if not valid.

``` Javascript
const breakfastSchema = new Schema({
  eggs: {
    type: Number,
    min: [6, "Too few eggs"], // error message
    max: 12,
    required: [true, "Why no eggs?"],
  },
  drink: {
    type: String,
    enum: ["Coffee", "Tea", "Water"], // allowed values
  },
});
```

#### Virtual Properties
Virtual properties are properties that you can get and set, but are not actually stored in the database. The getters are used to format/ combine fields, and setters are used to seperate a single value into multiple.

#### Creating/Searching records 
*Documents are called records in MongoDB*
To create a record, you can save the current instance of a model by using the save() method. You can also use create() and pass in objects as params to make a record.

To search for a record you can use query methods, specifying it as you would a JSON document. Like so:

```Javascript
const Athlete = mongoose.model("Athlete", yourSchema);

// find all athletes who play tennis, returning the 'name' and 'age' fields
const tennisPlayers = await Athlete.find(
  { sport: "Tennis" },
  "name age",
).exec();
```


### Routes and Controllers
![[Pasted image 20240307190012.png]]
This image highlights the flow of data and how a http request works. 
As you can see the controllers are functions used as the middle men between models, routes, and views.
**Routes** forward requests to the appropriate controller function.
**Controllers** get the requested data and display it.
**Views** are used by the controllers to render it.

```Javascript
// wiki.js - Wiki route module.

const express = require("express");
const router = express.Router();

// Home page route.
router.get("/", function (req, res) {
  res.send("Wiki home page");
});

// About page route.
router.get("/about", function (req, res) {
  res.send("About this wiki");
});

module.exports = router;
```

This code imports the Router() object, adds some routes using get(), and exports this object.
To use the router module in your main app you need to import it and app.use it

#### Route errors
The next() parameter can be used to pass errors, like so:

```js
router.get("/about", (req, res, next) => {
  About.find({}).exec((err, queryResults) => {
    if (err) {
      return next(err);
    }
    //Successful, so render
    res.render("about_view", { title: "About", list: queryResults });
  });
});
```
*if an error is returned then call next with an error message param*

#### Forms
A HTML Form is a group of inputs that can be used for a user to submit data to a database.
The **method** tag is used to specify the HTTP method used in a form, such as POST or GET.
The **action** tag is used as the destination the data is sent to.

![[Pasted image 20240307225308.png]]
This image shows that forms need to:
- Display the default form requested
- Recieve data submitted
- Validate and sanitize data
- If data is invalid, re-display form
- Else save data to database/return the search result
- Then redirect the user to a new page #### Validation and Sanitization Before the data from a form is stored it must be validated and sanitized, for security reasons. Validation checks the entered values are acceptable. Sanitization removes data that might be harmful to the server.


### API Basics
In recent years, a new way of structuring web apps has been being used. Instead of people creating an app that hosts both the database and view templates, many people are seperating these two parts, hosting the backend on a server and using something like github pages to host their frontend. Doing this makes your project more modular.

#### REST
REST stands for Representational State Transfer, and it is a way of structuring your API to make it more maintainable.

REST API's are resource based, that means that URI's will be structured like "/posts/:postid" instead of "/getPostComments"

#### Security
Securing your API is important, one way to do this is to pass a token between your front-end and your back-end. This allows us to verify the user's identity and time the user out if neccesary