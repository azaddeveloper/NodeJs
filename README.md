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
