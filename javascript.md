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

## closure
closure allows a function to access and manipulate variables that are external to that function.

```javascript
function Ninja() {
  // the scope of the variable is limited to inside the constructor function,
  // it's a "private" variable.
  var name = "who knows";
}
```

### usage
- mimic private vairables

## execution context stack

```
|                          |
| tryNextFunction('he')    |
|--------------------------|
| runFunction('lala')      |
|--------------------------|
| global execution context |
----------------------------
```

## variable definitions: `const`, `var`, `let`
`let` and `const` are introduced by ES6.
- `var`: mutable - it is defined in **the closest function** or **global lexical environment**. **blocks are ignored!**
- `const`: immutable, value can only be set once - it defines variables in the closest lexical environment (which can be a block, loop, a function, or even global environment)
- `let`: mutable - same as `const` above

## how does Javscript engine run and execute?
```javascript
const firstRobin = 'robin';
check(firstRobin);

function check(input) {
    console.log(`check ${input}`);
}
```
from the example above, function call `check(firstRobin)` will execute sucessfully, even though the actual `check()` function declaration is after the execution.

This only works for function declaration (i.e. `function() {}`, not `var a = function() {}`)

Although Javascript code is executed line by line, it turns out that Javascript engine "cheats" a little. It has two phases when running the code:
1. javascript engine **visits** and **registers** all declared variables within the current lexical environment.
2. javascript executes the code

## variable hoisting
variables are visited and registered in lexical environments before any code is executed.

## `promise`
A `promise` is a built-in type of objects that help you work with asynchronous code. A `promise` is a placeholder for a value that we don't have yet, but will at some later point. They are specially good for working with multiple asynchronous steps.

We can chaining promises with `then()`.

```javascript
const namePromise = new Promise(function(resolve, reject) {
  if (getJson().status === 200) {
    resolve('promise resolved');
  } else {
    reject('promised failed');
  }
});
```
disadvantages of callback:
1. difficult error handling
2. performing sequences of steps is tricky.
3. performing a number of steps in parallel is also tricky.

advantage of `promise`: 
1. simplifies the approache of dealing with asynchronous tasks.
2. can work with a sequence of handling

```javascript
function getJSON(url) {
  return new Promise((resolve, reject) => {
    const request = new XMLHttpRequest();
    request.open('GET', url);
    request.onload = function() {
      try {
        if (this.status === 200) {
          resolve(JSON.parse(this.response));
        } else {
          reject(this.status + ' ' + this.statusText);
        }
      } catch(e) {
        reject(e.message);
      }
    };
    
    request.onerror = function() {
      reject(this.status + ' ' + this.statusText);
    };
    
  });
}
```

## `async` and `await`
```javascript
(async function () {
  try {
    const ninjas = await getJSON('data/ninjas.json');
    const missions = await getJSON('data/missions.json');
    
    console.log(missions);
  } catch(e) {
    console.log('error: ' + e);
  }
})();
```


## `generator` (covered in Secrets of JavaSccript Ninja, working with generator functions section)
a `generator` is a function that generates a sequence of values. `generator` can receive standard arguments.

a `generator` works almost like a small program, a state machine that moves between states:
- **suspended start**
- **executing**
- **suspended yield**
- **completed**

calling the generator will create an object called an `iterator`. 

```javascript
function* NameGenerator() {
  yield 'Amy';
  yield 'Allen';
  yield 'Frank';
}

var nameIterator = NameGenerator();
nameIterator.next(); // Object: {value: 'Amy', done: 'false'}
```

### usage 1: generate ids
```javascript
function *IdGenerator() {
  let id = 0;
  while (true) {
    yield ++id;
  }
}
```

### usage 2: traverse the DOM
- recursion version:
```javascript
function traverseDOM(element, callback) {
  callback(element);
  element = element.firstElementChild;
  while (element) {
    traverseDOM(element, callback);
    element = element.nextElementSibling;
  }
}
```
- generator:
```javascript
function* DomTraversal(element) {
  yield element;
  element = element.firstElementChild;
  while (element) {
    yield* DomTraversal(element);
    element = element.nextElementSibling;
  }
}
```
