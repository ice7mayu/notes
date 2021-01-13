# JSON web Tokens

Read NPM [doc](https://www.npmjs.com/package/jsonwebtoken)

```bash
npm install jsonwebtoken
```

## Usage

```js
import jwt from "jsonwebtoken";

const privateKey = "my-private-key";

// To sign a token with a private key
const user = {name: "user1", role: "admin"};
const options = {expiresIn: "7d"};
const token = jwt.sign(user, privateKey, options);

// To verify and restore the user object from the token
const decodedUser = jwt.verify(token, privateKey);
// {name: "user1", role: "admin", iat: 1406234000}

// Will throw an error object with {name, message, [expiredAt]}
// err = {
//   name: 'TokenExpiredError',
//   message: 'jwt expired',
//   expiredAt: 1408621000
// };
```

## Generate a random private key with crypto

```js
import crypto from "crypto";

const key = crypto.randomBytes(64).toString('hex');

//'8ec49a80481caaed249dc63fc8d9be2c244f4a272f3112ee694b3679497d8d3b01b846637f6ec43606de1cbfbbe3aae656a498132c08a28fbb272257c9d0bd38'
```
