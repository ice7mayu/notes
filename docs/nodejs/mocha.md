# Use Mocha

Install Mocha via npm:

```bash
npm install --save-dev mocha
```

Run mocha in the terminal:

```bash
./node_modules/.bin/mocha
```

Set up a test script in package.json:

```json
"scripts": {
  "test": "mocha"
}
```

To pass argument to npm script:

```bash
npm test -- --timeout=3000
```

Or pass arguments in npm scripts:

```json
"scripts": {
  "test": "mocha --timeout=3000"
}
```

Example:

```js
import assert from "assert";

function queryDB() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const passed = true;
            if (passed) resolve({ users: ["user1", "user2", "user3"] });
            reject(new Error("Query DB failed"));
        }, 1000);
    });
}

describe("#Mocha Demo", function () {
    // Set timeout for this suite and nested suite and tests which do not override the value
    this.timeout(3 * 1000);

    describe("#Async tests", function () {
        it("just delay 500 ms", function (done) {
            setTimeout(() => {
                done();
            }, 500);
        });

        it.only("handle promise with done callback", function (done) {
            // run this test only
            queryDB()
                .then((result) => {
                    assert.equal(result.users.length, 3);
                    done(); // call done to move to the next test
                })
                .catch(done); // handle aysnc error
        });

        it("handle promise with async function", async function () {
            const result = await queryDB();
            assert.equal(result.users.length, 3);
        });

        it("dummy test should always pass", function () {});
    });
});

```

## Debug in VS Code

Go to **Debug View > Add Configuration > Node JS: Mocha Tests**

Pass in `bdd` if prefer BDD style (describe, it).

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [

        {
            "type": "node",
            "request": "launch",
            "name": "Mocha Tests",
            "program": "${workspaceFolder}/node_modules/mocha/bin/_mocha",
            "args": [
                "-u",
                "bdd",
                "--timeout",
                "999999",
                "--colors",
                "${workspaceFolder}/test"
            ],
            "internalConsoleOptions": "openOnSessionStart",
            "skipFiles": ["<node_internals>/**"]
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": ["<node_internals>/**"],
            "program": "${workspaceFolder}\\index.js"
        }
    ]
}

```
