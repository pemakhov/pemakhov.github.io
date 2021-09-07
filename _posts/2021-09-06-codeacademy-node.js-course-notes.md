---
layout: default
author: Serhii Pemakhov
---
# Codeacademy Node.js Course Notes

### 1. **REPL** - read - evaluate - print loop.

This is what the console in a browser's developer's tools is, or a node console in a terminal.

### 2. Editor in Node REPL

In node REPL every time you press `Enter`, the code evaluates. Type `.editor` to enter the editor mode.

### 3. The Process Module

A built-in module (doesn't require being required).

`process.memoryUsage()` - returns an object like this:

```
{
  rss: 37605376,
  heapTotal: 5574656,
  heapUsed: 4565648,
  external: 1678136,
  arrayBuffers: 9920
}
```

`process.memoryUsage().heapUsed` - returns the number of bytes used by the current process.

`process.argv` - returns the array containing arguments the current process was initiated with. The zero argument is the absolute path to the Node, which runs the process.

### 4. The OS Module

Not built-in module, therefore should be required like this:

```
const os = require('os');
```

`os.type()` — returns the computer’s operating system.

`os.arch()` — returns the operating system CPU architecture.

`os.networkInterfaces()` — returns information about the network interfaces of the computer, such as IP and MAC address.

`os.homedir()` — returns the current user’s home directory.

`os.hostname()` — returns the hostname of the operating system.

`os.uptime()` — returns the system uptime, in seconds.

### 5. The Util Module

Not built-in module, therefore should be required.

#### Types
Allows to check a type

```
const os = require('util');

const today = new Date();
const earthDay = 'April 22, 2022';
 
console.log(util.types.isDate(today));    // true
console.log(util.types.isDate(earthDay)); // false
```

#### Promisify
Allows to perform a callback function into promise.

### 6. Node Modules

**Modules** are reusable pieces of code in a file that can be exported and then imported for use in another file.
_The words “module” and “file” are often used interchangeably_

Module exports:

```
// my-module.js

const myFunction = () => {};
const anotherFunction = () => {};

module.exports.myFunction = myFunction;
module.exports.anotherFunction = anotherFunction;
```

Import:

```
const myModule = require('./my-module.js');
```

or

```
const { myFunction, anotherFunction } = require('./my-module.js');
```

### 7. The Events Module

```
// require events module
let events = require('events');

// a function to be called on the event
let listenerCallback = (data) => {
    console.log('Celebrate ' + data);
}

// create the instance of EventEmitter
const myEmitter = new events.EventEmitter();

// add the listener
myEmitter.on('celebration', listenerCallback);

// emit the event
myEmitter.emit('celebration', 'New Year');
```

### 8. Input / Output

`console.log` in Node.js is just a wrapper on `process.stdout.write()`.


```
// write to terminal
process.stdout.write('Hello world');

// read a user input
process.stdin.on('data', (userInput) => console.log(`Your input is ${userInput}`));
```

### 9. The Error Module

Many asynchronous functions use _error-first callback functions_ - callback functions which have an **error** as the first expected argument and **data** as the second argument.

```
const errorFirstCallback = (err, data)  => {
  if (err) {
    console.log(`Oops: ${err}`);
  } else {
    // err was falsy
    console.log(`Data: ${data}`);
  }
}
```

### 10. The Buffer Module

The buffer module is in the global scope.
**Buffer** objects are similar to the arrays of numbers from 0 to 255, each one represents a byte of data.

`.alloc` accepts three parameters:
- Size (required);
- Fill (optional, default is '0');
- Encoding (optional, default is UTF-8)

```
const buffer = Buffer.alloc(4);   // [0, 0, 0, 0]
```

`.toString` translates the buffer into a human-readable string. Takes three optional arguments:
- Encoding
- Start
- End

```
const buffer = Buffer.alloc(4, 'a');
console.log(buffer.toString()); // the output: aaaa
```

`.from` creates a buffer from a string or buffer
Accepts two arguments:
- Object (required) - an object to fill the buffer with
- Encoding (optional)

```
const buffer = Buffer.from('hello');
console.log(buffer); // output: [104, 101, 108, 108, 111]
```

`.concat` joins all methods buffer objects passed in an array into one buffer
Accepts two arguments:
- Array (required)
- Length (optional) - specifies the length of the concatenated buffer

```
const buffer1 = Buffer.from('hello'); // output: [104, 101, 108, 108, 111]
const buffer2 = Buffer.from('world'); // output:[119, 111, 114, 108, 100]
const array = [buffer1, buffer2];
const bufferConcat = Buffer.concat(array);
 
console.log(bufferConcat); // output: [104, 101, 108, 108, 111, 119, 111, 114, 108, 100]
```

### 11. The FS module

The technique when JavaScript in a browser has only limited access to the file system is called **sandboxing**.

```
const fs = require('fs');
 
let readDataCallback = (err, data) => {
  if (err) {
    console.log(`Something went wrong: ${err}`);
  } else {
    console.log(`Provided file contained: ${data}`);
  }
};
 
fs.readFile('./file.txt', 'utf-8', readDataCallback);
```

### 12. Streaming Data

Streaming data allows you to work with small pieces of data, not overloading the RAM.

Reading the file 'shoppingList.txt' line by line and printing out the data.
```
const readLine = require('readLine');
const fs = require('fs');

const myInterface = readLine.createInterface({
  input: fs.createReadStream('./shoppingList.txt')
});

const printData = (data) => console.log(`Item: ${data}`);

myInterface.on('line', printData);
```

Writing into a file.

```
const fs = require('fs')
 
const fileStream = fs.createWriteStream('output.txt');
 
fileStream.write('This is the first line!'); 
fileStream.write('This is the second line!');
fileStream.end();
```

### 13. The Timers Module

setTimeout, setInterval and setImmediate are functions of the global timer module.

### 14. The HTTP Module

```
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Server is running!');
});
 
server.listen(8080, () => {
  const { address, port } = server.address();
  console.log(`Server is listening on: http://${address}:${port}`);
})
```

### 15. URL Anatomy and URL Module

`https://website.com/articles?author=john&year=2020`

- https:// - protocol
- website.com - domain or host
- /articles - path
- author=john, year=2000 - key/value queries
- & query separator

```
const url = require('url');

const URL_TO_PARSE = 'https://www.example.com/p/a/t/h?prop1=value1&prop2=value2';

const myUrl = new URL(URL_TO_PARSE);

const { hostname, pathname, searchParams } = myUrl;

console.log(hostname); // output: example.com

myUrl.hostname = 'test.org';
myUrl.pathname = 'posts';
[...myUrl.searchParams.keys()].forEach((key) => myUrl.searchParams.delete(key));

console.log(myUrl.toString()); // output: https://test.org/posts
```

### 16. Routing

The http server accepts the request listener function. In this function you can handle the request according to the method:

```
const server = http.createServer((req, res) => {
  const { method } = req;
  switch(method) {
    case 'GET':
      return handleGetRequest(req, res);
    case 'POST':
      return handlePostRequest(req, res);
    default:
      throw new Error(`Unsupported request method: ${method}`);
  }
});
```

Then you can handle the route in a handler function:

```
const handleGetRequest = (req, res) => {
  const { pathname } = new URL(req.url);
  const data = { message: 'hello world' };

  if (pathname === '/users') {
    return res.end(JSON.stringify(data));
  }

  res.statusCode = 404;
  return res.end('bad request');
};
```

### 17. HTTP Status Codes

The HTTP Status Codes Classification:
1. Informational: 100...199
2. Successful: 200...299
3. Redirect: 300...399
4. Client Errors: 400...499
5. Server Errors: 500...599

#### Common Status Codes:
- 200 (OK)	This is the standard response for successful HTTP requests.
- 201 (CREATED)	This is the standard response for an HTTP request that resulted in an item being successfully created.
- 204 (NO CONTENT)	This is the standard response for successful HTTP requests, where nothing is being returned in the response body.
- 400 (BAD REQUEST)	The request cannot be processed because of bad request syntax, excessive size, or another client error.
- 403 (FORBIDDEN)	The client does not have permission to access this resource.
- 404 (NOT FOUND)	The resource could not be found at this time. It is possible it was deleted, or does not exist yet.
- 500 (INTERNAL SERVER ERROR)	The generic answer for an unexpected failure if there is no more specific information available.

#### Status Codes By Method:
- GET — return 200 (OK)
- POST — return 201 (CREATED)
- PUT — return 200 (OK)
- DELETE — return 204 (NO CONTENT) If the operation fails, return the most specific status code possible corresponding to the problem that was encountered.
 
### 18. REST

REST - REpresentational State Transfer

In REST the Client and the Server can be developed independently as long, as they know what format of messages they can send to each other.

Statelessness - neither the Client, nor the Server should know the state of the other side.

#### The basic REST methods:
- GET - retrieve a specific resource by id, or a collection of resources
- POST - create a new resource
- PUT - update a specific resource (by id)
- DELETE - remove a specific resource by id

A **media type** (also known as a Multipurpose Internet Mail Extensions or **MIME type**) is a standard that indicates the nature and format of a document, file, or assortment of bytes. It is defined and standardized in IETF's _RFC 6838_
The simplest MIME type consists of a _type_ and _subtype_ separated by a **/**
An optional parameter can be added to provide additional details

```
type/subtype;parameter=value
```

#### MIME types:
- text: text/html, text/css, text/plain
- image: image/png, image/jpeg, image/gif
- audio: audio/wav, audio/mpeg
- video: video/mp4, video/ogg
- application: application/json, application/pdf, application/xml, application/octet-stream

When clients send request, they mention the content type they can receive in the **Accept** filed. As well server, sending responses should send the **content type** header.

#### Paths
`fashionboutique.com/customers/223/orders/12` accessing an order with id=12 of customer with id=223
`fashionboutique.com/customers/:id` delete (for example) a customer by id

#### Examples of Requests and Responses:
1. When we want to view all customers
Request:

```
GET http://fashionboutique.com/customers
Accept: application/json
```

a possible response header:

```
Status Code: 200 (OK)
Content-type: application/json
```

2. Create a new customer
Request:

```
POST http://fashionboutique.com/customers
Body:
{
  “customer”: {
    “name” = “Scylla Buss”,
    “email” = “scylla.buss@codecademy.org”
  }
}
```

Response header:

```
201 (CREATED)
Content-type: application/json
```

3. View a single customer
Request:

```
GET http://fashionboutique.com/customers/123
Accept: application/json
```

Response:

```
Status Code: 200 (OK)
Content-type: application/json
```

4. Update a customer:
Request:

```
PUT http://fashionboutique.com/customers/123
Body:
{
  “customer”: {
    “name” = “Scylla Buss”,
    “email” = “scyllabuss1@codecademy.com”
  }
}
```

A possible response header would have Status Code: 200 (OK)

5. Delete a customer by id
Request:

```
DELETE http://fashionboutique.com/customers/123
```

The response would have a header containing Status Code: 204 (NO CONTENT)

