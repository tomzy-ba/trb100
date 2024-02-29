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


