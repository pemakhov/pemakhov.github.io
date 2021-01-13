---
layout: default
author: Serhii Pemakhov
---
Recently I have encountered a problem with approaching data stored in an object, from my express application. The object received data from redis. Therefore this object was created asyncronously.
For some time I persisted trying to do it this way:
```
let myDatabase = {};

```
