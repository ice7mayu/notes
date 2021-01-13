# JavaScript `.call()` `.apply()` and `.bind()` — explained

These 3 functions are all designed to set **CONTEXT**, or more specifically, what `this` refers to.

```js
var owen = {
    name: "Owen"
}
function sayTo(first, second) {
    console.log(this);
    return first + " " + this.name + " " + second;
}
sayTo(owen, "Hi", "how are you?");

//returns "[Object] undefined Hi"
```

The first argument, `owen`, goes to the first variable, “hi” goes to the second variable, and “how are you?” goes nowhere, and `this.name` is undefined, because this is **NOT** the object `owen`.

Using `.call()`, the notation is as follows:

```text
functionName.call(value of this, arg1, arg2…)
```

```js
var owen = {
    name: "Owen"
}
function sayTo(first, second) {
    console.log(this);
    return first + " " + this.name + " " + second;
}
sayTo.call(owen, "Hi", "how are you?");
//this is now the owen object
//returns "Hi Owen how are you?"
```

Using `.apply()`, the format is as follows:

```text
functionName.apply(value of this, [arg1, arg2 …])
```

For `.apply()` to work, arguments 1 and 2 need to be entered as an array.

```js
sayTo.apply(owen, ["Hi", "how are you?"]);
```

Using `.bind()`

`.bind()`, unlike `.apply()` and `.call()`, returns a function instead of a value.

`.bind()` sets the value of `this` and changes the function to a new function, but it doesn’t invoke the function.

```js
var owen = {
    name: "Owen"
}
function sayTo(first, second) {
    return first + “ “ + this.name + “ “ + second;
}
var sayToOwenFunction = sayTo.bind(owen);
sayToOwenFunction('hi', 'how are you');
```

Summary

```js
.call()
Function.call(value of this, arg1, arg2, …)
//Will execute Function

.apply()
Function.apply(value of this, [arg1, arg2, ..])
//Will execute Function

.bind()
newFunction = Function.bind(value of this, arg1, arg2 …)
//Will return a new function
```
