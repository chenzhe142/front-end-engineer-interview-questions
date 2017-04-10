# Object

## Array

### Detecting array
  1. `Array.isArray()` <= recommended
  2. `array instanceof Array`

### Stack method
  1. `.push()`
  2. `.pop()`

### Queue method
  1. `.unshift()` => enqueue
  2. `.shift()` => dequeue

### Reordering
  1. `.reverse()`
  2. `.sort()`
    - to accomplish a correct sort, pass a callback function to it.

### Manipulation method
  1. `.concat()`
  2. `.slice(startPos, endPos)`
    - if no params, return a copy
    - if `startPos`, return `list[startPos:]`
    - if `startPos` and `endPos`, return `list[startPos:endPos]`. endPos is not included
    
  3. `.splice()`
  
    - deletion
`.splice(positionToDelete, numberOfElementToDelete)`

    - insertion
`.splice(positionToInsert, 0, elements)`

    - replacement
`.splice(positionToReplace, 1, element)`

### Location methods
item must be strictly equal as if compared using `===`

  1. `.indexOf()`
  2. `.lastIndexOf()`

### Iterative methods

### `Array.prototype.map` vs `Array.prototype.forEach`
`.map` method creates a new array with the results of calling a provided function on every element in this array.
`.forEach` excutes a callback function for each element


### `Array.from()`
Creates a new Array instance from an array-like or iterable object.

### `Array.prototype.concat` - don't change the existing array, returns a new array.
Used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

`arr.reduce(callback, [initialValue])`

```javascript
// callback: (accumulator, currentValue)
// - accumulator: previously returned value
// - currentValue

var sum = [0, 1, 2, 3].reduce(function(acc, val) {
  return acc + val;
}, 0);
// sum is 6

var list1 = [[0, 1], [2, 3], [4, 5]];
var list2 = [0, [1, [2, [3, [4, [5]]]]]];

const flatten = arr => arr.reduce(
  (acc, val) => acc.concat(
    Array.isArray(val) ? flatten(val) : val
  ),
  []);
flatten(list1); // returns [0, 1, 2, 3, 4, 5]
flatten(list2); // returns [0, 1, 2, 3, 4, 5]

// ES5
var flatten2 = function(array) {
    return array.reduce(function(acc, val) {
        return acc.concat(Array.isArray(val) ? flatten2(val) : val);
    }, []);
};

// iterative:
var list1 = [[0, 1], [2, 3], [4, 5]];
var list2 = [0, [1, [2, [3, [4, [5]]]]]];

var flatten = function(array) {
    let i = 0;

    var queue = array.slice();
    var result = [];

    while (queue.length > 0) {
        const val = queue.shift();
        if (Array.isArray(val)) {
            queue = val.concat(queue);
        } else {
            result.push(val);
        }
    }

    return result;
};

var a = flatten(list1);
console.log(a);

var b = flatten(list2);
console.log(b);
```
