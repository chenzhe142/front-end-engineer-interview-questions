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

***

## Scope

***

## Memory
