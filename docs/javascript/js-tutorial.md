# JavaScript Tutorial

## for-in vs for-of

The `for-in` loop should not be used to iterate over an array where the index order is important. The `for-in` loop is optimized for iterating over object's properties, you should better use a for loop with a numeric index or `for-of` loop.
The `for-of` loop doesn't work with objects because they are not iterable. If you want to iterate over the properties of an object you can use the `for-in` loop.

## Manipulate items in an array

The `push()` and `pop()` methods runs faster than `unshift()` and `shift()`. Because `push()` and `pop()` methods simply add and remove elements at the end of an array therefore the elements do not move, whereas `unshift()` and `shift()` add and remove elements at the beginning of the array that require re-indexing of whole array.

## indexOf and lastIndexOf

`Array.indexOf(searchElement, fromIndex)`

- `indexOf`: Returns the first index of the match (searches from the fromIndex to the end).
- `lastIndexOf`: Returns the last index of the match (searches from the beginning to the fromIndex).

## Sort a numeric array

The `sort()` method sorts the numeric array elements by converting them to strings. To fix this by providing a compare function:

```javascript
let a = [1, 5, 2, 11, 8]

console.log(a)  // [ 1, 11, 2, 5, 8 ]

a.sort(function (a, b) {
  return a - b
})

console.log(a)  // [ 1, 2, 5, 8, 11 ]
```

- If the compare function returns a value less than 0, then a comes first.
- If the compare function returns a value greater than 0, then b comes first.
- If the compare function returns 0, a and b remain unchanged with respect to each other, but sorted with respect to all other elements.

## Function Declaration and Function Expression

```javascript
declaration(); // Outputs: Hi, I'm a function declaration!
function declaration() {
    alert("Hi, I'm a function declaration!");
}

expression(); // Uncaught TypeError: undefined is not a function
var expression = function() {
    alert("Hi, I'm a function expression!");
};
```

JavaScript parse declaration function before the program executes. Therefore, it doesn't matter if the program invokes the function before it is defined because JavaScript has **hoisted** the function to the top of the current scope behind the scenes. The function expression is not evaluated until it is assigned to a variable; therefore, it is still undefined when invoked.

## Function Hoisting

Functions that are defined using a function declaration are automatically hoisted.

```javascript
// Calling function before declaration
sayHello(); // Outputs: Hello, I'm hoisted!

function sayHello() {
    alert("Hello, I'm hoisted!");
}
```

Similarly, the variable declarations are also hoisted to the top of their current scope automatically.

```javascript
str = "Hello World!";
console.log(str); // Outputs: Hello World!
var str;
```

JavaScript only hoists declarations, not initializations. That means if a variable is declared and initialized after using it, the value will be `undefined`

```javascript
console.log(str); // Outputs: undefined
var str;
str = "Hello World!";
```

## Borrowing Methods from Objects

- `call(thisObj, arg1, arg2, ...)`
- `apply(thisObj, [argsArray])`

```javascript
// These are equivalent
Math.max(1, 2, 3);
Math.max.apply(null, [1, 2, 3]);
Math.max(...[1, 2, 3]);
```

## Closure

A closure is basically an inner function that has access to the parent function's scope, even after the parent function has finished executing.
Closures internally store references to their outer variables, and can access and update their values.

## IIFE (Immediately Invoked Function Expression)

An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined.

```javascript
(function () {
    statements
})(parameters);
```

It is a design pattern which is also known as a **Self-Executing Anonymous Function** and contains two major parts:

- The first is the anonymous function with lexical scope enclosed within the *Grouping Operator* `()`. This prevents accessing variables within the IIFE idiom as well as polluting the global scope.
- The second part creates the immediately invoked function expression `()` through which the JavaScript engine will directly interpret the function.

## JSON Parsing

`JSON.parse()` and `JSON.stringify()`

## Arrow Functions

Provides a more concise syntax for writing function expressions by opting out the `function` and `return` keywords.

```javascript
let sum = (a, b) => a + b;
console.log(sum(1, 2));
```

An arrow function does not have its own `this`, it takes `this` from the outer function where it is defined. In JavaScript, `this` is the current execution context of a function.

There is an important difference between regular functions and arrow functions. Unlike a normal function, an arrow function does not have its own `this`, it takes `this` from the outer function where it is defined. In JavaScript, `this` is the current execution context of a function.

```javascript
function Person(name) {
  this.name = name;
  this.getInfo = function () {
    return () => {
      // Refers to the outer name
      console.log(this.name);
    };
  };
}

let person = new Person('person');
let printInfo = person.getInfo();

printInfo();
```

## The rest parameter

A rest parameter is specified by prefixing a named parameter with rest operator (`...`).
Rest parameter can only be the last one in the list of parameters, and there can only be one rest parameter.

```javascript
function myFunction(a, b, ...args) {
    // args is an Array which is of type object
    return args;
}
```

## The Spread Operator

The spread operator (`...`) spreads out (i.e. splits up) an array and passes the values into the specified function.

```javascript
function addNumbers(a, b, c) {
    return a + b + c;
}
addNumbers(...[1, 2, 3])
```

## The array destructuring assignment

```javascript
let fruits = ['Apple', 'Banana', 'Mango'];
let [a, ...r] = fruits;

console.log(a); // Apple
console.log(r); // [ 'Banana', 'Mango' ]
```

## The object destructuring assignment

```javascript
let person = {name: "Peter", age: 28};
let {name, age} = person;

console.log(name);  // Perter
console.log(age);  // 28
```
