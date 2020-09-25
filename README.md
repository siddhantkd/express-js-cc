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


