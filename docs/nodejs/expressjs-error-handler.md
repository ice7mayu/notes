# ExpressJS Error Handling

- [Official Doc](https://expressjs.com/en/guide/error-handling.html)

## How to handle error

If synchronous code throws an error, then Express will catch and process it. For example:

```js
app.get('/', function (req, res) {
  throw new Error('BROKEN') // Express will catch this on its own.
})
```

For errors returned from asynchronous functions invoked by route handlers and middleware, you must pass them to the `next(error)` function, while `error` is the instance of Error. Express will catch and process them. For example:

```js
app.get('/', function (req, res, next) {
  fs.readFile('/file-does-not-exist', function (err, data) {
    if (err) {
      next(err) // Pass errors to Express.
    } else {
      res.send(data)
    }
  })
})
```

Starting with Express 5, route handlers and middleware that return a Promise will call `next(value)` automatically when they reject or throw an error.

## Writing error handlers

Define error-handling middleware functions in the same way as other middleware functions, except error-handling functions have four arguments instead of three: (err, req, res, next). For example:

```js
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

## Note

Calls to `next()` and `next(err)` indicate that the current handler is complete and in what state. `next(err)` will skip all remaining handlers in the chain except for those that are set up to handle errors as described above.
