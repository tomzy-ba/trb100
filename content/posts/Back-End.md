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


### Routes
A web app needs:
- Routes, to forward requests to the appropriate controller function
- Controller functions, to get the requested data and create the HTML file
- Views(Templates), to render the data

A route is a section of Express code that associates a HTTP verb like GET, a URL path, and a function. express.Router can be used to set this up.

Route Parameters are **named** URL segments used to capture values at specific positions in the URL. The named segments are prefixed with a colon and then the name like: "/:example_parameter/". The captured values are stored in the req.params object using the parameter names as keys.

```Javascript
app.get("/users/:userId/books/:bookId", (req, res) => {
  // Access userId via: req.params.userId
  // Access bookId via: req.params.bookId
  res.send(req.params);
});
```




### Databases



Database API's are asynchronous, which means methods return immediate promises and other code can be executed in the meantime.
#### Models
A database model defines how your data is structured, organized, and used within a database. 
When designing your models it is good practice to have seperate models for each "object".

### Mongoose

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
    min: [6, "Too few eggs"],
    max: 12,
    required: [true, "Why no eggs?"],
  },
  drink: {
    type: String,
    enum: ["Coffee", "Tea", "Water"],
  },
});
```

#### Virtual Properties
Virtual properties are properties that you can get and set, but are not on MongoDB. The getters are used to format/ combine fields, and setters are used to seperate a single value into multiple.

#### Creating/Searching records 
*Documents are called records in MongoDB*
To create a record, you can save the current instance of a model by using the save() method. You can also use create() and pass in objects as params to make a record.

To search for a record you can use query methods, specifying the as you would a JSON document. Like so:

```Javascript
const Athlete = mongoose.model("Athlete", yourSchema);

// find all athletes who play tennis, returning the 'name' and 'age' fields
const tennisPlayers = await Athlete.find(
  { sport: "Tennis" },
  "name age",
).exec();
```
