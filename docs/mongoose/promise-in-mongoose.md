# Promises in Mongoose

[Mongoose Tutorials](https://masteringjs.io/mongoose)

Mongoose has built-in support for promises. In Mongoose 5, async operations like `.save()` and `.find().exec()` return a promise **unless** you pass a callback.

```js
const Model = mongoose.model('Test', Schema({
  name: String
}));

const doc = new Model({ name: 'Neo' });

const promise = doc.save();  // will return a Promise
promise instanceof Promise; // true

const res = doc.save(function callback(err) {
  /*...*/
});
res; // undefined if pass in a callback function
```

## Queries are not Promises

While `save()` returns a promise, functions like Mongoose's `find()` return a Mongoose `Query`.

```js
const query = Model.find();

query instanceof Promise; // false
query instanceof mongoose.Query; // true
```

Mongoose queries are **thenables**. In other words, queries have a `then()` function that behaves similarly to the **Promise** `then()` function. So you can use queries with **promise chaining** and `async/await`.

```js
// Using queries with promise chaining
Model.findOne({ name: 'Mr. Anderson' }).
  then(doc => Model.updateOne({ _id: doc._id }, { name: 'Neo' })).
  then(() => Model.findOne({ name: 'Neo' })).
  then(doc => console.log(doc.name)); // 'Neo'

// Using queries with async/await
const doc = await Model.findOne({ name: 'Neo' });
console.log(doc.name); // 'Neo'
```
