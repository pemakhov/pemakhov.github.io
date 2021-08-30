---
layout: default
author: Serhii Pemakhov
---
# Codeacademy Node.js Course Notes

## 1. **REPL** - read - evaluate - print loop.
This is what the console in a browser's developer's tools is, or a node console in a terminal.

## 2. Editor in Node REPL
In node REPL every time you press `Enter`, the code evaluates. Type `.editor` to enter the editor mode.

## 3. The Process Module
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

## 4. The OS Module
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

## 5. The Util Module
Not built-in module, therefore should be required.

### Types
Allows to check a type

```
const os = require('util');

const today = new Date();
const earthDay = 'April 22, 2022';
 
console.log(util.types.isDate(today));    // true
console.log(util.types.isDate(earthDay)); // false
```

### Promisify
Allows to perform a callback function into promise.

## 6. Node Modules

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
