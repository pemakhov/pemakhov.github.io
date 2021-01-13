---
layout: default
author: Serhii Pemakhov
---
Recently I have encountered a problem with approaching data stored in an object, from my express application. The object received data from redis. Therefore this object was created asyncronously.
For some time I persisted trying to do it this way:
```
let myDatabase = {};
MyDatabase.init().then((db) => myDatabase = db);
export default {
  myDatabase,
};
```
It didn't work. In the components myDatabase was imported before it was rewritten. Therefore it always was `{}`.
The solution is just to create the empty collection and then fill it in with data without rewriting the object. Therewore the created links pointed to the same object.
```
export const myDatabase = MyDatabase.init();
dataManager.getDataFromRedis().then((data) => MyDatabase.fillIn(data));
```
