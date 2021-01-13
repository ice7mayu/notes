# JavaScript Info Note

## Jsdoc Cheat Sheet

[Jsdoc cheat sheet](https://devhints.io/jsdoc)

## Strict Equality Operator === checks the equality without type conversion.

Strict Equality Operator `===` checks the equality without type conversion.
In other words, if `a` and `b` are of different types, then `a === b` immediately returns false without an attempt to convert them.

```javascript
alert( 0 === false ); // false, because the types are different
```

## Comparison with null and undefined

For a non-strict check `==`. There’s a special rule. These two are a “sweet couple”: they equal each other (in the sense of `==`), but not any other value.

```javascript
alert( null == undefined ); // true
alert( null === undefined ); // false
```

## Boolean conversion

The Boolean conversion rules:

- A number `0`, an empty string `""`, `null`, `undefined`, and `NaN` all become false. Because of that they are called **“falsy”** values.
- Other values become true, so they are called **“truthy”**.

## Conditional operator ‘?’

```javascript
let result = condition ? value1 : value2;
```

## OR `||` finds the first truthy value

```javascript
result = value1 || value2 || value3;
```

The OR `||` operator does the following:

- Evaluates operands from left to right.
- For each operand, converts it to boolean. If the result is `true`, stops and returns the original value of that operand.
- If all operands have been evaluated (i.e. all were `false`), returns the last operand.

```javascript
let currentUser = null;
let defaultUser = "John";

let name = currentUser || defaultUser || "unnamed";

alert( name ); // selects "John" – the first truthy value
```

## Double NOT `!!`

A double NOT `!!` is sometimes used for converting a value to boolean type:

```javascript
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

## Switch Case Strict Equality Check

The value of `x` is checked for a strict equality to the `value`:

```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

## Computed properties

We can use square brackets in an object literal. That’s called *computed properties*.

```javascript
let fruit = "apple";

let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit
};

alert( bag.apple ); // 5 if fruit="apple"
```

## Property value shorthand

```javascript
function makeUser(name, age) {
  return {
    name, // same as name: name
    age,  // same as age: age
    // ...
  };
}
```

## `this` is not bound

The value of `this` is evaluated during the run-time, depending on the context.

```javascript
let user1 = {
  name: "user1",
  hi,
};
let user2 = {
  name: "user2",
  hi,
};

function hi() {
  // this is the object who calls the function
  console.log(`${this.name} says hi`);
}

user1.hi();
user2.hi();
```

## Arrow functions have no `this`

Arrow functions are special: they don’t have their “own” this. If we reference this from such a function, it’s taken from the outer “normal” function.

```javascript
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // Ilya
```

## Mixin

```javascript
// mixin
let sayHiMixin = {
  sayHi() {
    alert(`Hello ${this.name}`);
  },
  sayBye() {
    alert(`Bye ${this.name}`);
  }
};

// usage:
class User {
  constructor(name) {
    this.name = name;
  }
}

// copy the methods
Object.assign(User.prototype, sayHiMixin);

// now User can say hi
new User("Dude").sayHi(); // Hello Dude!
```

## Async / Await

```javascript
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 1000)
  });

  let result = await promise; // wait until the promise resolves (*)

  alert(result); // "done!"
}

f();
```
