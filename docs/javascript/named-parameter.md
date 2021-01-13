# Named Parameter

[Named parameters in JavaScript and ECMAScript 6](https://2ality.com/2011/11/keyword-parameters.html)

## Default positional parameters

```js
function add(a = 10, b = 3) {
  return a + b;
}

add(); // 13
add(100); // 103 - skip the 2nd param
add(null, 100) // 103 - can't skip the 1st param
```

## Default named parameters

Define a function with named parameters and default value:

```js
function namedParameters(
    err = "defaultError",
    { arg1 = "arg1DefaultValue", arg2 = "arg2DefaultValue" } = {}
) {
    console.log(`err=${err}`);
    console.log(`arg1=${arg1}`);
    console.log(`arg2=${arg2}`);
}

namedParameters();
// err=defaultError
// arg1=arg1DefaultValue
// arg2=arg2DefaultValue

namedParameters(null, {});
// err=null
// arg1=arg1DefaultValue
// arg2=arg2DefaultValue

namedParameters(undefined, { arg1: 1 });
// err=defaultError
// arg1=1
// arg2=arg2DefaultValue

namedParameters("err", { arg2: 2 });
// err=err
// arg1=arg1DefaultValue
// arg2=2

namedParameters("err", { arg2: 3, arg1: 4 });
// err=err
// arg1=4
// arg2=3
```
