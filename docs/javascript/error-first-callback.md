# DEFINING AN ERROR-FIRST CALLBACK

[The Node.js Way - Understanding Error-First Callbacks](http://fredkschott.com/post/2014/03/understanding-error-first-callbacks-in-node-js/)

There’s really only two rules for defining an error-first callback:

1. **The first argument of the callback is reserved for an error object.** If an error occurred, it will be returned by the first `err` argument.
2. **The second argument of the callback is reserved for any successful response data.** If no error occurred, `err` will be set to null and any successful data will be returned in the second argument.

```js
fs.readFile('/foo.txt', function(err, data) {
  // If an error occurred, handle it (throw, propagate, etc)
  if(err) {
    console.log('Unknown Error');
    return;
  }
  // Otherwise, log the file contents
  console.log(data);
});
```
