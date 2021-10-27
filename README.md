# NodeJs

# What is NodeJs where we can use it.
Node.js is an extremely powerful framework developed on Chrome’s V8 JavaScript engine that compiles the JavaScript directly into the native machine code. It is a lightweight framework used for creating server-side web applications and extends JavaScript API to offer usual server-side functionalities. It is generally used for large-scale application development, especially for video streaming sites, single page application, and other web applications.

# How does Node.js work?
A web server using Node.js typically has a workflow that is quite similar to the diagram illustrated below. Let’s explore this flow of operations in detail.
Clients send requests to the webserver to interact with the web application. Requests can be non-blocking or blocking:
- Querying for data
- Deleting data 
- Updating the data
- Node.js retrieves the incoming requests and adds those to the Event Queue
- The requests are then passed one-by-one through the Event Loop. It checks if the requests are simple enough not to require any external resources
- The Event Loop processes simple requests (non-blocking operations), such as I/O Polling, and returns the responses to the corresponding clients
  A single thread from the Thread Pool is assigned to a single complex request. 
This thread is responsible for completing a particular blocking request by accessing external resources, such as computation, database, file system, etc.

Once the task is carried out completely, the response is sent to the Event Loop that sends that response back to the client.
![image](https://user-images.githubusercontent.com/40568415/138236347-4de1676c-aa79-40a3-a4c0-40bed527d4bb.png)

# What does the runtime environment mean in Node.js?
The Node.js runtime is the software stack responsible for installing your web service's code and its dependencies and running your service.

The Node.js runtime for App Engine in the standard environment is declared in the app.yaml file:
``
runtime: nodejs10
``
# What are the data types in Node.js?
Primitive Types
- String
- Number
- Boolean
- Undefined
- Null
- RegExp
- Buffer: Node.js includes an additional data type called Buffer (not available in browser's JavaScript). Buffer is mainly used to store binary data, while reading from a file 
  or receiving packets over the network.

# How to create a simple server in Node.js that returns Hello World?

**Step 01**: Create a project directory
```
mkdir myapp
cd myapp
```

**Step 02**: Initialize project and link it to npm
```
npm init
```
This creates a package.json file in your myapp folder. The file contains references for all npm packages you have downloaded to your project. The command will prompt you to enter a number of things. You can enter your way through all of them EXCEPT this one:
```
entry point: (index.js)
```
Rename this to:
```
app.js
```
**Step 03**: Install Express in the myapp directory
```
npm install express --save
```
**Step 04**: app.js
```
var express = require('express');
var app = express();
app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
```
**Step 05**: Run the app
```
node app.js  
```
# What is the diffrence between synchronous and asynchronous.

In **synchronous** operations tasks are performed one at a time and only when one is completed, the following is unblocked. In other words, you need to wait for a task to finish to move to the next one. 

In **asynchronous** operations, on the other hand, you can move to another task before the previous one finishes. This way, with asynchronous programming you’re able to deal with multiple requests simultaneously, thus completing more tasks in a much shorter period of time.   

# Explain callback in Node.js.
  Node. js, being an asynchronous platform, doesn't wait around for things like file I/O to finish Node. js uses callbacks. A callback is a function called at the completion of   a given task; this prevents any blocking, and allows other code to be run in the meantime.
  ```
  function printString(){
   console.log("Tom"); 
   setTimeout(function()  { console.log("Jacob"); }, 300); 
  console.log("Mark")
  }

  printString();
  ```
  
 # What is callback hell in Node.js?
  Callback hell is a phenomenon that afflicts a JavaScript developer when he tries to execute multiple asynchronous operations one after the other.

  An asynchronous function is one where some external activity must complete before a result can be processed; it is “asynchronous” in the sense that there is an unpredictable   amount of time before a result becomes available. Such functions require a callback function to handle errors and process the result.
  ```
  async_A(function(){
   async_B(function(){
       async_C(function(){
           async_D(function(){
           ....
           });
       });
     });
  });
  ```
  Techniques for avoiding callback hell
  - Using Async.js
  - Using Promises
  - Using Async-Await
 # Callback is syncronous or asyncoronous
 Basically - if a callback does all it's work before returning to the caller, it's "synchronous". If it can return to the caller immediately after it's invoked - and the caller 
 and the callback can work in parallel - then it's "asynchronous". The problem with synchronous callbacks is they can appear to "hang".

# What is Promise.
Promise is use to handle the result of an asynchronous task once it has completed or encountered an error. Promises make writing asynchronous code easier. They’re an improvement on the callback pattern.
The core idea behind promises is that a promise represents the result of an asynchronous operation. A promise is in one of three different states:

- pending - The initial state of a promise.
- fulfilled - The state of a promise representing a successful operation.
- rejected - The state of a promise representing a failed operation. Once a promise is fulfilled or rejected, it is immutable (i.e. it can never change again).

Creating a Promise
```
var myPromise = new Promise(function(resolve, reject){
   ....
})
```
# What is promise chaining 
 Promise chaining is a syntax that allows you to chain together multiple asynchronous tasks in a specific order. This is great for complex code where one asynchronous task 
 needs to be performed after the completion of a different asynchronous task.
```
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10);
    }, 3 * 100);
});

p.then((result) => {
    console.log(result);
    return result * 2;
}).then((result) => {
    console.log(result);
    return result * 3;
});
```
# What are the advantages of using promises instead of callbacks?
The main advantage of using promise is you get an object to decide the action that needs to be taken after the async task completes. This gives more manageable code and avoids callback hell.

# What is async await in Nodejs?
With Node v8, the async/await feature was officially rolled out by the Node to deal with Promises and function chaining. The functions need not to be chained one after another, simply await the function that returns the Promise. But the function async needs to be declared before awaiting a function returning a Promise.

Await is basically syntactic sugar for Promises. It makes your asynchronous code look more like synchronous/procedural code, which is easier for humans to understand.

Syntax of Async and Await:
```
async function printMyAsync(){
  await printString("one")
  await printString("two")
  await printString("three")
}
```
# Why is Node.js Single-threaded?
Node.js is single-threaded for async processing. By doing async processing on a single-thread under typical web loads, more performance and scalability can be achieved instead of the typical thread-based implementation.

# Is it possible to achieve multithreading in NodeJS?
No, you can't use threads in node.js. It uses asynchronous model of code execution. Behind the asynchronous model, the node itself uses threads. But as far as I know, they can't be accessed in the app without additional libraries.With the asynchronous model you don't actually need threads. 

# how to achive multi threading in NodeJS?
# NodeJS really single threaded or not?
# What is Event loop in Node.js? How does it work?
# What is REPL? What purpose it is used for?
- Read: It reads the inputs from users and parses it into JavaScript data structure. It is then stored to memory.
- Eval: The parsed JavaScript data structure is evaluated for the results.
- Print: The result is printed after the evaluation.
- Loop: Loops the input command. To come out of NODE REPL, press ctrl+c twice

# How can you make sure your dependencies are safe?

The only option is to automate the update / security audit of your dependencies. For that there are free and paid options:
- npm outdated
- Trace by RisingStack
- NSP
- GreenKeeper
- Snyk
- npm audit
- npm audit fix

# What are some of the most popular packages of Node.js?
- **Async**: Async is a utility module which provides straight-forward, powerful functions for working with asynchronous JavaScript.
- **Browserify**: Browserify will recursively analyze all the require() calls in your app in order to build a bundle you can serve up to the browser in a single <script> tag.
- **Bower**: Bower is a package manager for the web. It works by fetching and installing packages from all over, taking care of hunting, finding, downloading, and saving the stuff you’re looking for.
- **Csv**: csv module has four sub modules which provides CSV generation, parsing, transformation and serialization for Node.js.
- **Debug**: Debug is a tiny node.js debugging utility modelled after node core's debugging technique.
- **Express**: Express is a fast, un-opinionated, minimalist web framework. It provides small, robust tooling for HTTP servers, making it a great solution for single page applications, web sites, hybrids, or public HTTP APIs.
- **Grunt**: is a JavaScript Task Runner that facilitates creating new projects and makes performing repetitive but necessary tasks such as linting, unit testing, concatenating and minifying files (among other things) trivial.
- **Gulp**: is a streaming build system that helps you automate painful or time-consuming tasks in your development workflow.
- **Hapi**: is a streaming build system that helps you automate painful or time-consuming tasks in your development workflow.
Http-- **server**: is a simple, zero-configuration command-line http server. It is powerful enough for production usage, but it's simple and hackable enough to be used for testing, local development, and learning.
- **Inquirer**: A collection of common interactive command line user interfaces.
- **Jquery**: jQuery is a fast, small, and feature-rich JavaScript library.
- **Jshint**: Static analysis tool to detect errors and potential problems in JavaScript code and to enforce your team's coding conventions.
- **Koa**: Koa is web app framework. It is an expressive HTTP middleware for node.js to make web applications and APIs more enjoyable to write.
- **Lodash**: The lodash library exported as a node module. Lodash is a modern JavaScript utility library delivering modularity, performance, & extras.
- **Less**: The less library exported as a node module.
- **Moment**: A lightweight JavaScript date library for parsing, validating, manipulating, and formatting dates.
- **Mongoose**: It is a MongoDB object modeling tool designed to work in an asynchronous environment.
- **MongoDB**: The official MongoDB driver for Node.js. It provides a high-level API on top of mongodb-core that is meant for end users.
- **Npm**: is package manager for javascript.
- **Nodemon**: It is a simple monitor script for use during development of a node.js app, It will watch the files in the directory in which nodemon was started, and if any files change, nodemon will automatically restart your node application.
- **Nodemailer**: This module enables e-mail sending from a Node.js applications.
- **Optimist**: is a node.js library for option parsing with an argv hash.
- **Phantomjs**: An NPM installer for PhantomJS, headless webkit with JS API. It has fast and native support for various web - **standards**: DOM handling, CSS selector, JSON, Canvas, and SVG.
- **Passport**: A simple, unobtrusive authentication middleware for Node.js. Passport uses the strategies to authenticate requests. Strategies can range from verifying username and password credentials or authentication using OAuth or OpenID.
- **Q**: Q is a library for promises. A promise is an object that represents the return value or the thrown exception that the function may eventually provide.
- **Request**: Request is Simplified HTTP request client make it possible to make http calls. It supports HTTPS and follows redirects by default.
Socket.- **io**: Its a node.js realtime framework server.
- **Sails**: - **Sails** : API-driven framework for building realtime apps, using MVC conventions (based on Express and Socket.io)
- **Through**: It enables simplified stream construction. It is easy way to create a stream that is both readable and writable.
- **Underscore**: Underscore.js is a utility-belt library for JavaScript that provides support for the usual functional suspects (each, map, reduce, filter...) without extending any core JavaScript objects.
- **Validator**: A nodejs module for a library of string validators and sanitizers.
- **Winston**: A multi-transport async logging library for Node.js
- **Ws**: A simple to use, blazing fast and thoroughly tested websocket client, server and console for node.js
- **Xml2js**: A Simple XML to JavaScript object converter.
- **Yo**: A CLI tool for running Yeoman generators
- **Zmq**: Bindings for node.js and io.js to ZeroMQ .It is a high-performance asynchronous messaging library, aimed at use in distributed or concurrent applications.
