# event

## event handling

We can use the `v-on` directive to **listen** to DOM events and run some JavaScript when they’re triggered

## dom event object

HTML DOM events allow JavaScript to register different event handlers on elements in an HTML document.

[dom event tutorial](https://www.w3schools.com/jsref/dom_obj_event.asp)

Like onclick event.

## event modifiers

- `.prevent`: event will no longer reload the page
- `.stop`: event's propagation will be stopped
- `.capture`
- `.self`
- `.once`
- `.passive`

## key modifiers

- `.enter`
- `.alt`

## two-way data banding

`v-model`: create two-way data bindings on form input, textarea, and select elements.

## computed

`Computed properties` are cached, and only re-computed on reactive dependency changes. Computed properties have to return something.

## v-bind

## v-if and v-show

- `v-if` or `v-else-if` display one branch for once time.
- `v-show` display all branch info.

## v-for

## component

custom element

## ref

Add ref for elements and component.

## main.js file

the entry file of vue,The main role is to initialize the vue instance and use the required plugins

## index.html

index is a container hosting component.

## App.vue

root component can import vue file

## scoped

When a `<style>` tag has the scoped attribute, its CSS will apply to elements of the current component only.

## props

## primitive and reference

In JavaScript, a variable may store two types of values: primitive and reference.
JavaScript provides six primitive types as undefined, null, boolean, number, string, and symbol , and a reference type object.

If the value is a primitive value, when you access the variable, you manipulate the actual value stored in that variable. In other words, the variable that stores a primitive value is accessed by value.

Unlike a primitive value, when you manipulate an object, you work on the reference of that object, rather than the actual object. It means a variable that stores an object is accessed by reference.

## custom event emit

```js
this.$emit("myEvent");
```

## event bus

The event bus is used to solve the communication problem between father, son and brother events.

## slots

[slots tutorial](https://juejin.im/post/5a69ece0f265da3e5a5777ed)
