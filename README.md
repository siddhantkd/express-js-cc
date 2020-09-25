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

# Setting up our app

* Create package.json ```javascript npm init```
* Install express ```javascript npm i express```
* Create index.js
* Install nodemon for auto update of server ```javascript npm i nodemon```



