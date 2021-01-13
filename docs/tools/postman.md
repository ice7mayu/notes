# Postman scripting API test

Postman Makes API Development Simple.

Developers use Postman to build
modern software for the API-first world.

Click [here](https://learning.getpostman.com/docs) to view doc.

## Collections

Postman organizes APIs in collections and folders. You can either run a single request or the whole collection.

## Examples

You can add examples to an API to demonstrate different payload and response for various scenarios.

## Script

You can add variable place holder `{{var}}` in `header` or `body` sections.

You can read or write variables in `Pre-req` or `Tests` sections.

Scripts in `Pre-req` section will be executed before sending the API request, e.g

```javascript
// To set a local variable.
pm.variables.set("key", "value");
```

Scripts in `Tests` section will be executed after sending the API request.

```javascript
// To read a local variable from pre-req section or previous step.
let k = pm.variables.get("key");

//To run a test after sending the API request.
pm.test("test script goes here", function () {
    pm.expect(pm.response.text()).to.include("success");
});
```

## Workflow

You can run a whole collection with all the requests within it by default execution order.

Or you can script to run with logic control.

```javascript
// To run a specific request within the same collection.
postman.setNextRequest("request_name");

// To end subsequent requests.
postman.setNextRequest(null);
```

## Postman Console

View logs through Postman console.

## Export Data

- Export the whole workspace.
- Export a collection.
- Export environment variables.

## Import Data

- Import single file.
- Import folder.

The End