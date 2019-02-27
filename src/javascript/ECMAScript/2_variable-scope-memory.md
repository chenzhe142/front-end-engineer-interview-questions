# Variables, Scope. and Memory

***

## Variables

### variables contain 2 types of data:
  1. primitive values:
    - simple atomic pieces of data
    - you'll be manipulating the real data
    - primitive values can't have properties added to them even though attempting to do so won't cause an error. In strict mode, it will throw `TypeError` for cannot create property
  2. reference values:
    - objects that may be made up of multiple values
    - when manipulating an object, you're really working on a `reference` to that object rather than the actual object itself.
    - reference values can have properties.

### when copying values:
  1. primitive values:
    - the value stored on the variable object is **created** and **copied** into the location for the new variable.
    - the new value is completely separate from the old one. It can be used with no side effect.
  2. reference values:
    - the new value is actually a pointer to an object stored on the heap.

### argument passing:
- all arguments in ECMAScript are passed by value.
- if the value is primitive, then it acts just like a primitive value.
- if the value is a reference, it acts just like a reference variable copy.
- think of function arguments as nothing more than **local variables**.

### determine type
- `typeof` is used for identifying primitive type.
- `instanceof` is used for reference variables.
- all reference values, by definition, are instances of `object`.
- if `instanceof` operator is used with a primitive value, it will always return `false`, because primitives aren't objects.

***

## Execution Context & Scope
- the execution context of a variable or a function defines what other data it has access to, as well as how it should behave.
- the global execution context is depended on the host environment.
- each function has its own execution context.
  - after the function has finished executing, the stack is poped, returning control to the previously executing context.
- `scope chain`: when code is executed in a context, the scope chain is created.
  - the purpose is to provide ordered access to all variables and functions that an execution context has access to.
  - an inner context can access everything from all outer contexts through the scope chain, but the outer context cannot access the inner context.
- `scope chain` augmentation
  - the `catch` block in a `try-catch` statement
  - a `with` statement
- when a variable is declared using `var`, it's automatically added to the most immediate context available.
- if a variable is initialized without first being declared, it gets **added to the global context automatically**.
  - in strict mode, it will cause an error.
- identifier lookup:
  - to look up a variable in function, the search starts at the front of the `scope chain`, looking for an identifier with the given name. If not, go to the previous one.
  - **it is faster to access local variable than global variables, because there is no search ip the scope chain.**

***

## Garbage collection
- javascript is a garbage-collected language. the executing environment is responsible for managing the memory required during code execution.
- collector runs periodically
- 2 strategies:
  - mark-and-sweep (**mostly used**)
    - variables that go out of scope will automatically be marked for reclamation and will be deleted during the garbage-collection process.
  - reference-counting
    - it keeps track of how many references there are to a particular value. javascript engines no longer use this algorithm.
    - the issue is still around with IE.
    - it causes problems when circular references exist in code

***

## Memory
- the amount of memory available for use in web browsers is typically **much less** than is available for desktop applications.
- keeping the amount of used memory to a minimum leads to better page performance.
- when data is no longer necessary, it's best to set the value to `null`
