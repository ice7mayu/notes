# Bcrypt

A library to help you hash passwords.

Read NPM [doc](https://www.npmjs.com/package/bcrypt)

## Installation

```shell
npm install bcrypt
```

## Usage Example

```js
import bcrypt from "bcrypt";
const ROUNDS = 10;

// To hash with default 10 rounds
const plainPassword = "password";
const hash = bcrypt.hashSync(plainPassword, ROUNDS);

// To compare clear text to hash
bcrypt.compareSync(plainPassword, hash) // true
bcrypt.compareSync("other password", hash) // false
```
