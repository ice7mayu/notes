# Switching out callbacks with promises in Mongoose

## Bad

```js
// error first callback style
User.findById('123', function(err, user) {
  if (err) {
    return console.log('error:', err);
  }

  user.name = 'Robert Paulson';

  user.save(function(err) {
    // yet another err object to deal with
    if (err) {
      return console.log('error:', err);
    }
    console.log('updated user: ' + user.name);
    // do something with updated user
  });
});
```

## Good

Use Promise instead:

```js
var promise = User.findById('123').exec();

promise.then(function(user) {
  user.name = 'Robert Paulson';

  return user.save(); // returns a promise
})
.then(function(user) {
  console.log('updated user: ' + user.name);
  // do something with updated user
})
.catch(function(err){
  // just need one of these
  console.log('error:', err);
});
```
