# JavaScript

## `Array.prototype.map` vs `Array.prototype.forEach`
`.map` method creates a new array with the results of calling a provided function on every element in this array.
`.forEach` excutes a callback function for each element

## `Array` vs `Object`
Array is object, but object is not array. Array is based on object, with its own unique prototype methods.



## strict mode: `use strict`
It disables `arguments` params. It changes the behavior of Javascript engines so that errors are thrown instead of silently picked up.

## invoking functions
**When a function is invoked, two implicit parameters are passed to the function, `arguments` and `this`.**

- `this` - represents the function context, the object on which our function is invoked.

- `arguments` - a collection of parameters passed to a function. It's an array-like object, but not array.

### as a function - `fly()`
```javascript
function ninja() {
  return this; // this => window object
}

function ninja() {
  "use strict"; // in strcit mode, javascript engine will not pass window parameter to the function
  return this; // this => undefined
}
```

### as a method - `ninja.fly()`
When a function is assigned to a property of an object, it would be invoked by referencing the function using that property. The function is invoked as a `method` of that object.

### as a constructor, creating a new objet - `new Ninja()`
1. a new empty object is created
2. this object is passed to the constructor as the `this` parameter, and it will become the constructor's function context.
3. the newly constructed object is returned as the `new` operator's value.

#### what happens if not using `new` operator to construct an object?
In nonstrict mode, the `this` parameter will refer to `window` object. You may not invoke functions properly.


### via function's `apply()` or `call()` methods - `fly.call(ninja)` or `fly.apply(ninja)`
- `.apply(this, [arguments])` - the object to be used as function context, **an array of values** to be used as the invocation arguments.
- `.call(this, arguments)` - the object to be used as function context, **arguments that are passed directly into the argument list**.

## `Function.prototype.apply` vs `Function.prototype.call`
- `.apply(this, [arguments])` - the object to be used as function context, **an array of values** to be used as the invocation arguments.
- `.call(this, arguments)` - the object to be used as function context, **arguments that are passed directly into the argument list**.

## ES6 - arrow function
arrow functions do not get their own implicit `this` parameter when we call them. They remember the value of the `this` parameter at the time they were created.

**Exception**: If an arrow function is defined within an object literal that is defined in global code, the value of the `this` parameter associated with the arrow function is the global `window` object.

## `Function.prototype.bind()`
`.bind()` is designed to **create** and return a **new** function that is bound to the passed-in object. It creates a completely new function.

