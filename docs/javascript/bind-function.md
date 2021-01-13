# The Bind Function

[See this blog](https://www.tjvantoll.com/2015/12/29/console-error-bind/).

In JavaScript, `this` within a function call is determined by how the function is called. If it's called as part of an expression retrieving an object property (e.g., `foo.bar()` calls `bar()` as part of a property retrieval operation getting it from foo), `this` is set to the object that the property came from during the call to the function.

The `bind()` lets you **create a new function** with its `this` value set to a provided value. For instance, the code below shows how to change the `this` value of a simple function from the `window` object to an object created on the fly:

```js
const logger = function() { console.log(this.name); }
logger();  // Logs "", as the window object has no name property
const tj = logger.bind({ name: "TJ" });
tj();  // Logs "TJ"
```

More example:

```js
function printInfo() {
    console.log(`Name = ${this.name}, Age = ${this.age}`);
}

const hina = {
    name: "hina",
    age: 15,
    printInfo,
};

const hodaka = {
    name: "hodaka",
    age: 16,
};

hina.printInfo();  // Name = hina, Age = 15

hodaka.printInfo = printInfo;
hodaka.printInfo();  // Name = hodaka, Age = 16

const printHodakaInfo = printInfo.bind(hodaka);
printHodakaInfo();  // Name = hodaka, Age = 16

hodaka.printInfo = printInfo.bind(hina);
hodaka.printInfo();  // Name = hina, Age = 15
```
