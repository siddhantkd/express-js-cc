# Express-js-cc
Repository for getting acquainted with express JS.

## What is Express
* Fast , unopinionated , minimalistic  web framework for Node.js 
* Server-Side framework
* Combined with React JS, Angular JS to build full stack applications 

## Why Express

* Makes Node.js application easier 
* Used for both server rendered applications and API/Microservices 
* Fast, light, free
* Full control of request and response 

## Pre-Requisites 

* JS, ES6
* Basic Node.js and npm(node package manager)

## Before getting into code - Requirements 
* Node.js
* Postman

## Basic Server Syntax

```javascript
const express = require('express');

//Init Express

const app = express();

//Create endpoints/route handlers

app.get('/', function(req,res) {
 res.send('Hello Bilahi');
});

//Listen to a port 

app.listen(8000);

```
* The require() method is used to load and cache JavaScript modules. So here it is used to bring express to the top.
* To initialise express we put the express() method to a variable usually called app.
* We are accepting a Get request to the index route '/' and we use a callback function.
* Responding with a text hello world. 
* Listening to the port 8000. 
* http://localhost:8000/ Will show the response of get request. 

## Basic Route Handling 

```javascript 
app.get('/', function(req,res) {
 
//Fetch from database
//MongoDB, mySQL, etc can be used 
//Load Pages
//Return JSON Data
//Full access to Request and Response

});

```
* Request object - HTTP Request parameters - URLparameters, query
* Response object - HTTP Response - Send back JSON Data, Render a template, redirect etc
* We can parse incoming data with Body Parser
* No need to store routes in one file. Express has a router that can store routes in seperate files and export them 

## Express Middleware 

* Middleware functions are functions which have access to request and response object. 
* Express has built in middleware.
* Middleware also third party. 
* Custom Middleware - Making changes to request and response object, Ending response cycle, Calling next middleware in the stack, 

## Setting up our app

* Create package.json ```npm init```
* Install express ```npm i express```
* Create index.js
* Install nodemon for auto update of server ```npm i nodemon```

## Starting a simple express Server 

```javascript 
const express = require("express");
const app = express();
const PORT = process.env.PORT || 8000;
app.listen(PORT, () => console.log("Server Started"));
```

## Creating a Route
```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Responding to request <br><h1>Hello World </h1>");
});

const PORT = process.env.PORT || 8000;
app.listen(PORT, () => console.log("Server Started"));

```

### Note 

* Everytime anything is changed the server needs to be stopped and restarted 
* For the above problem - Install nodemon ```npm i -D nodemon```
* ```-D``` in the above code is we want nodemon development only it will not work in production.
* After installation change scripts in package.json

```javascript
"scripts": {
    "start": "node index",
    "dev": "nodemon index"
  },
```
* Start the server ```npm run dev```

## Sending a HTML file in response 

```javascript
const express = require("express");
const path = require("path");

const app = express();

app.get("/", (req, res) => {
  res.sendFile(path.join(__dirname, "public", "index.html"));
});

const PORT = process.env.PORT || 8000;
app.listen(PORT, () => console.log("Server Started"));

```

## Setting a folder as static folder

```javascript
const express = require("express");
const path = require("path");

const app = express();

//Set Static folder

app.use(express.static(path.join(__dirname, "public")));

const PORT = process.env.PORT || 8000;
app.listen(PORT, () => console.log("Server Started"));

```
### Note

* Just works like a static site with contents inside public folder

## Creating a REST API 

```javascript 

const members = [
  {
    id: 1,
    name: "Madara Uchiha",
    email: "madara@gmail.com",
    status: "active",
  },
  {
    id: 2,
    name: "Obito Uchiha",
    email: "obi@gmail.com",
    status: "inactive",
  },
  {
    id: 3,
    name: "Kakashi Hatake",
    email: "Kakashi@gmail.com",
    status: "active",
  },
];

app.get("/api/members", (req, res) => {
  res.json(members);
});

```

* We want to return this json when we hit route 
* This can be done by react or angular or in postman 
* POSTMAN is used here to hit the route and get the members

## Middleware - Creating a logger 

```javascript 
const moment = require("moment");

const logger = (req, res, next) => {
  console.log(
    `${req.protocol}://${req.get("host")}${
      req.originalUrl
    }: ${moment().format()}`
  );
  next();
};

module.exports = logger;

```
* We are creating a middleware function logger that takes in (req, res, next)
* We are loging the URL thats hit and the date. 
* The URL is access is using request object ```req.protocol``` this will give us HTTP, Then we type ```://``` and get the host ```req.get("host")``` after that we get the original URL ```req.originalUrl```.
* If we go to postman and send a request and look in the console. We'd get the whole URL that's hit. ```http://localhost:5000/api/members```
* For date install moment using npm ```npm i moment``` and require is using ```require()``` method at the top.
* ```${moment().format()}``` gives the date

## Getting a single member from member database with ID

```javascript
app.get("/api/members/:id", (req, res) => {
  res.json(members.filter((member) => member.id === parseInt(req.params.id)));
});
```
#### Note

* req.params.id is string so we need to parseInt() it to match the data type of member ID from database

### If member of that particular ID doesn't exist the way we set up our API is on us. ex: 

```javascript 

//Get Single Member
app.get("/api/members/:id", (req, res) => {
  const found = members.some((member) => member.id === parseInt(req.params.id));
  if (found) {
    res.json(members.filter((member) => member.id === parseInt(req.params.id)));
  } else {
    res.status(400).json({ msg: `No Member with the ID of ${req.params.id}` });
  }
});

```

* ```req.status(400)``` - Gives 400 Bad Request with the message incuded in ```json({msg:})```

## Routes folder for the routes 

Note - 

* Having all the routes in a single file might get messy.
* We move all the routes to a folder - router>api>members.js
* In order to use the routes we need to require express and router at the top

```javascript 
const express = require('express')
const router = express.Router()
const members = require("../../Members");

```
* ```../../``` is to get out of api>routes and and into the main root because our Members database is in that folder
* In our index.js we replace the routes with 

```javascript 
app.use("/api/members", require("./routes/api/members"));
```
* Since we are using ```/api/members``` in our index.js app.use code we can replace ```/api/members``` in routes which are in routes folder with ```/``` .

## POST Request - Creating New entries in Database(Members)

**When we add something or create something to the server -  POST request**

* use ```router.post``` 

```javascript 
router.post("/", (req, res) => {
  const newMember = {
    res.send(req.body)
  };

```
*  ```/``` to hit the ```api/members```
* ```(req,res) => {} ``` callback function
* uuid is a npm package that generates a random user id ```npm i uuid``` and bring it in our members ```const uuid = require('uuid')```
* To parse the data we are sending in we need a body parser

```javascript
//body parser middleware
app.use(express.json())
app.use(express.urlencoded(extended: false))
```
Now -
```javascript 
//Create Member
router.post("/", (req, res) => {
  const newMember = {
    id: uuid.v4(),
    name: req.body.name,
    email: req.body.email,
    status: "active",
  };

  if (!newMember.name || !newMember.email) {
    return res.status(400).json({ msg: "Please include a name and email" });
  }
  members.push(newMember);
  res.json(members);
});
```
* For the name property, we'll get that from the request body ```req.body.name```
* For the email ```req.body.email```
* Then we push the newMember in our hardcoded database(array) and return the whole array




