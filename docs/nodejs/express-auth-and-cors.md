# Express Basic Authentication and CORS

## Basic Authentication

Write a middleware for basic authentication.

Extract Authentication from request header which is a base64 encoded string.

```js
app.use((req, res, next) => {
  // As authentication handler
  const basicAuth = req.headers["authorization"];
  if (basicAuth === "Basic bWF5dToxMjM0NTY=") {
    next();
  } else {
    res.status(401).json({ message: "Invalid user or password" });
  }
});
```

Or use npm package. NPM [doc](https://www.npmjs.com/package/express-basic-auth)

```bash
npm install express-basic-auth
```

```js
app.use(
  basicAuth({
    users: {
      admin: "supersecret",
      adam: "password1234",
      eve: "asdfghjkl",
    },
    unauthorizedResponse: { error: "Invalid username or password" },
  })
);
```

The middleware will check incoming requests to have a basic auth header matching one of the three passed credentials and response a custom error message.

## CORS

NPM [doc](https://www.npmjs.com/package/cors)

Installation.

```bash
npm install cors
```

Simple Usage

```js
var express = require('express')
var cors = require('cors')
var app = express()

app.use(cors())

app.get('/products/:id', function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for all origins!'})
})

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
})
```
