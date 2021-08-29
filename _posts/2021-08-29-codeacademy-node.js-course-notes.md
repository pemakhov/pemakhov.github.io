---
layout: default
author: Serhii Pemakhov
---
# Codeacademy node.js course notes

## 1. **REPL** - read - evaluate - print loop.
This is what the console in a browser's developer's tools is, or a node console in a terminal.

## 2. Editor in node REPL
In node REPL every time you press `Enter`, the code evaluates. Type `.editor` to enter the editor mode.

## 3. The Process module
`process.memoryUsage()` returns an object like this:

```
{
  rss: 37605376,
  heapTotal: 5574656,
  heapUsed: 4565648,
  external: 1678136,
  arrayBuffers: 9920
}
```

`process.memoryUsage().heapUsed` returns will return the number of bytes used by the current process.

`process.argv` returns the array containing arguments the current process was initiated with. The zero argument is the absolute path to the Node, which runs the process.
