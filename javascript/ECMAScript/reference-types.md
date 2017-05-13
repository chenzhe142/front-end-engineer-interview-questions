# Object

阅读：https://github.com/creeperyang/blog/issues/7

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
    - 为了实现排序，sort()会调用每个数组项的toString()转型方法，然后比较得到的字符串，以确定如何排序，即使数组中的每一项都是数值，sort()方法比较的也是字符串

### Manipulation method
  1. `.concat()`
    - 这个方法会先创建当前array的一个副本，然后将接收到的参数添加到这个copy的末尾，最后返回新构建的数组。
    - 在没有parameter时，返回一个copy
    - 如果是数组，会将数组中的每一项copy过去，
    - 如果不是数组，直接添加
  2. `.slice(startPos, endPos)`
    - 不会影响原数组
    - if no params, return a copy
    - if `startPos`, return `list[startPos:]`
    - if `startPos` and `endPos`, return `list[startPos:endPos]`. endPos is not included

  3. `.splice()`
    - 始终都会返回一个数组

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

参数：要查找的项，开始查找的index

### Iterative methods
以下方法都不会修改array中所包含的值

  1. `.every()`

  2. `.filter()`

  3. `.forEach()`

  4. `.map()`

  5. `.some()

### `Array.prototype.map` vs `Array.prototype.forEach`
`.map` method creates a new array with the results of calling a provided function on every element in this array.
`.forEach` excutes a callback function for each element


### 缩小方法
1. `reduce()`
2. `reduceRight()`

这两个方法接受两个参数：在每一项上调用的函数，作为缩小基础的初始值

### `Array.from()`
Creates a new Array instance from an array-like or iterable object.


## String

### Check substring
  1. `String.prototype.includes(substring)`

### Check char & substring
  1. `String.prototype.indexOf(char)`
  1. `String.prototype.indexOf(substring)`

### Remove trailing & front whitespace
  1. `.trim()`
  2. `.trimLeft()`
  3. `.trimRight()`

### Ascii <=> Char
  1. `s.charCodeAt(index)`
  2. `String.fromCharCode(asciiCode)`

## Math

### Rounding
  1. `Math.ceil`
  2. `Math.floor`
  3. `Math.round`

### Randomize
  1. `Math.random`

### Others
  1. `Math.abs()`
  2. `Math.exp()` e的m次幂
  3. `Math.log()` 自然对数
  4. `Math.pow(num, power)`
  5. `Math.sqrt()`

## Map
Map is added in ECMAScript 2015.
[MDN - Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

Objects have been used as Maps historically. However, there are important differences between Objects and Maps that make using a Map better:
  - easily to get `.size` for a Map
  - the key of objects is only allowed for `String` and `Symbol`. Map allows any values, including function, objects, and any primitive.

### performance: `object` vs `map`
according to [Jsperf - object vs map](https://jsperf.com/es6-map-vs-object-properties/2), `map` is faster and more suitable for performing as a `hashmap`

### methods
  1. `.set(key, value)`
  2. `.has(key)`
  3. `.keys()`
  4. `.delete(key)`
  5. `.clear()`
  6. `.size()`

## Set
Set is added in ECMAScript 2015.
[MDN - Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

### methods
  1. `.length`
  2. `.add(value)`
  3. `.clear()`
  4. `.delete(value)`
  5. `.has(value)`
  6. `.keys()`
