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
``
mkdir myapp
cd myapp
``

**Step 02**: Initialize project and link it to npm
``
npm init
``
This creates a package.json file in your myapp folder. The file contains references for all npm packages you have downloaded to your project. The command will prompt you to enter a number of things. You can enter your way through all of them EXCEPT this one:
``
entry point: (index.js)
``
Rename this to:
``
app.js
``
**Step 03**: Install Express in the myapp directory
``
npm install express --save
``
**Step 04**: app.js
``
var express = require('express');
var app = express();
app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
``
**Step 05**: Run the app
``
node app.js  
``
