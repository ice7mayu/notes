# Manage Environment Variables in your NodeJs Application with dotenv

## Refs

- [Original Post](https://itnext.io/manage-environment-variables-in-your-nodejs-application-with-dotenv-520914a9254b)
- [Official Git Repo](https://github.com/motdotla/dotenv)

## What is dotenv? Why use dotenv

**Dotenv** is a module that we will use to access environment variables in our application. When a NodeJs application runs, it injects a global variable called `process.env` which contains information about the state of environment in which the application is running. Dotenv will allow us to load our environment variables stored in the .env file into `process.env`.

## How to use dotenv

Install dotenv via npm:

```bash
npm install dotenv
```

Create a *.env* file in your application root directory:

```bash
touch .env
```

Add some environment variables to *.env* file:

```ini
# content of .env

PORT=3000
APP_SECRET="THIS_IS_TOP_SECRET"
```

Import dotenv module as soon as possible in your application:

```javascript
import dotenv from 'dotenv';
dotenv.config();

// Access environment variables in your code:
console.log(process.env.PORT);
console.log(process.env.APP_SECRET);
```

## Conditionally load

### 1. Check the condition in your code

```javascript
import dotenv from "dotenv";

if (!process.env.NODE_ENV || process.env.NODE_ENV === "development") {
    // Loads '.env' only if NODE_ENV already exists or missing
    dotenv.config();
}
```

### 2. Preload in the command line option

```bash
node -r dotenv/config your_script.js
```

## FAQ

### Should I commit my .env file

No. We **strongly** recommend against committing your *.env* file to version control. It should only include environment-specific values such as database passwords or API keys. Your production database should have a different password than your development database.

### What happens to environment variables that were already set

We will never modify any environment variables that have already been set. In particular, if there is a variable in your *.env* file which collides with one that already exists in your environment, then that variable will be skipped. This behavior allows you to override all *.env* configurations with a machine-specific environment, although it is not recommended.
