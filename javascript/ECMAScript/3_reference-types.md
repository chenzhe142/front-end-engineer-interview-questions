# Reference Types

阅读：https://github.com/creeperyang/blog/issues/7

## Object

`Object` is a reference type. By using `new` operator, it creates an instance of `Object` reference type.

```javascript
const person = new Object();
```

这行代码创建了`Object`的一个新instance，并把其存储在`person` variable中。使用的constructor是`Object`，它只为new instance定义了默认的property和function。

虽然Object instance不具备多少功能，但对于在application中存储和传输数据而言，它们确实是非常理想的选择

```
const person = {
  "name": 'adam',
  age: 3
};
```
在最后一个property后加`,`，会在IE7以及更早的版本和opera中导致错误。

```javascript
function getCar(brand, options = {}) {
  this.brand = brand;
  this.color = options.color || 'red';
}
```

在传递大量optional parameter的时候推荐用object包裹住，必要的parameter使用命名参数。


## Array

- Array的length可以进行动态调整
- 在使用Array constructor时可以省略new，结果是一样的。
- `.length` is not read-only. You can modify the value to **add** or **remove** values from the array.


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

Callback function accepts 4 parameters:
- `prev`
- `current`
- `index`
- `array`

### `Array.from()`
Creates a new Array instance from an array-like or iterable object.

## Date

## RegExp

## Function
function实际上是object，每个function都是Function类型的instance，而且都与其他reference type一样具有属性和方法。由于function是object，因此function name实际上也是一个指向函数对象的指针，不会与某个函数绑定。

ECMAScript没有函数重载的概念。

函数重载（overload）：是Ada、C++、C#、D和Java等编程语言中具有的一项特性，这项特性允许创建数项名称相同但功能的输入输出类型不同的子程序，它可以简单地称为一个单独功能可以执行多项任务的能力。
```java
public class Overloading {
    public int test(){
        System.out.println("test1");
        return 1;
    }

    public void test(int a){
        System.out.println("test2");
    }   

    //以下两个参数类型顺序不同
    public String test(int a,String s){
        System.out.println("test3");
        return "returntest3";
    }   

    public String test(String s,int a){
        System.out.println("test4");
        return "returntest4";
    }   

    public static void main(String[] args){
        Overloading o = new Overloading();
        System.out.println(o.test());
        o.test(1);
        System.out.println(o.test(1,"test3"));
        System.out.println(o.test("test4",1));
    }
}
```

## 函数声明和函数表达式

JavaScript engine会先读取函数声明，`function abc()`，并使其在执行任何代码前可用，至于函数表达式，`var a = function()`，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。这个过程叫做function declaration hoisting，读取并将函数声明添加到executive context中。

## 作为value的函数
因为ECMAScript中的函数名本身就是变量，所有函数也可以作为value来使用。也就是说，不仅可以像传递参数一样把一个function传递给另一个function，而且可以将function当作return value。

## 函数内部的property

- `arguments`：类数组对象，包含着传入函数中的所有参数
  - 同时包含一个名叫`callee`的指针，指向拥有这个arguments对象的函数
- `this`：指向的是函数据以执行的环境对象
- `caller`：指向调用当前函数的函数

值得注意的是，`caller`和`callee`在严格模式下会报错，这是为了加强这门语言的安全性，这样第三方代码就不能在相同的环境里窥视其他代码了。

## 函数属性和方法

- `.length`：函数希望接收的命名参数的个数
- 每个function都包含两个非继承而来的方法，`apply()`和`call()`。这两个方法的用途都是在特定的execution context中调用函数。实际上等于设置function内`this`对象的值。
  - `apply()`: `this`, `[]`
  - `call()`: `this`, arguments

***

# 特殊的reference type: 基本包装类型（primitive wrapper type）。它们本质上是function。

## Boxing wrappers

这些类型与本章介绍的其他reference type相似，但同时也具有与各自的基本reference type相应的特殊行为。实际上，每当读取一个primitive type的value的时候，后台就会创建一个对应的基本包装类型的对象，从而能让我们能够调用一些方法来操作这些数据。

```javascript
var s1 = '1234356';
var s2 = s1.substring(2);
```

在以上的例子中，`s1`是一个string的primitive type。我们知道，primitive type不是object，因而逻辑上讲它们不应该有方法。

其实，为了让我们实现这种直观的操作，后台已经自动完成了一系列的处理。当第二行代码访问`s1`时，访问过程中处于一种读取模式，也就是要从内存中读取这个字符串的值。

而在读取模式中访问字符串时，后台都会自动完成下列处理：
  1. 创建`String`类型的一个instance
  2. 在instance上调用指定的方法
  3. 销毁这个instance

以上三个步骤等价于：
```javascript
var s1 = new String('some text');
var s2 = s1.substring(2);
s1 = null;
```

经过此番处理，基本的字符串就变得跟object一样了。而且，上面三个步骤也分别适用于`Boolean`和`Number`类型对应的布尔值和数字值。

reference type和primitive wrapper type的主要区别就是**object的生存期**。使用`new`创建的reference type的实例，在执行流离开当前作用域之前一直保存在内存中。而自动创建的primitive wrapper type的对象只存在于一行代码的执行瞬间，然后立即被销毁。

这意味着我们不能在运行时为primitive value添加属性和方法。

```javascript
var s1 = 'some text';
s1.color = 'red'; // 创建的string对象在这行之后就被销毁了
alert(s1.color);  //undefined
```

**尽量避免使用`new String()`创建string**，因为这种做法很容易让人分不清自己是在处理primitive type还是reference type。理由如下：
```javascript
var a = '123';
var b = new String('123');

typeof a // "string"
typeof b // "object"
```

## Boolean
建议：永远不要使用`Boolean`对象

## Number
Number类型重写了`valueOf()`, `toLocaleString()`和`toString()`方法。重写后的`valueOf()`返回对象表示的基本类型的数值，另外两个方法则返回字符串形式的数值。

- `toString(进制)`
- `toFixed(小数的数量)`：可以表示带有0到20个小数位的数值，但这只是标准实现的范围，有些浏览器也可能支持更多位数。
- `toExponential()`： 科学计数法
- `toPricision()`：可能返回`toFixed()`，或`toExponential()`
- `Number.isInteger()`: 测试是否是整数
- `Number.isSafeInteger(..)`: 测试是否安全的整数。

建议：永远不要使用`Number`对象

## String
`String`是string的对象包装类型。

### 字符方法：
Return `UTF-16 code unit` of a char.

Unicode code points range from 0 to 1114111 (0x10FFFF). The first 128 Unicode code points are a direct match of the ASCII character encoding. For information on Unicode, see the JavaScript Guide.

  1. `.charCodeAt(index)`
  2. `.fromCharCode(utfCode)`
  3. `.charAt(index)`
  4. use `[]`

### 字符串操作方法
<!-- todo: add notes for negative indices -->
  1. `.concat()`，返回新拼接的string，等于使用`+`
  2. `.slice()`: startIndex, 子字符串最后一个字符后面的位置
  3. `.substr()`: startIndex, 返回的字符个数
  4. `.substring()`: startIndex, 子字符串最后一个字符后面的位置
  5. `.localeCompare()`：这个方法比较两个字符串，并返回一个值。
    - 小于：-1
    - 等于: 0
    - 大于: 1

### Check substring
  1. `.includes(substring)`

### 字符串位置方法
  1. `.indexOf(char, startIndex)`
  1. `.indexOf(substring, startIndex)`

### `trim()`方法
  1. `.trim()`
  2. `.trimLeft()`
  3. `.trimRight()`

### 字符串大小写转换方法
  1. `toLowerCase()`
  2. `toLocaleLowerCase()`
  3. `toUpperCase()`
  4. `toLocaleUpperCase()`

### 字符串的模式匹配方法
  1. `.match()`：本质上与调用`RegExp`的`exec()`方法相同，其只接受一个parameter，要么是一个正则表达式，要么是一个RegExp对象。返回一个数组。
  2. `.search()`：返回字符串中第一个匹配项的index，如果没有，则返回-1
  3. `.replace()`：第一个参数（正则表达式，string），第二个参数是要替换的内容（string, function）。如果第一个参数是string，则只会替换第一个子字符串。
  4. `.split()`：这个方法可以基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中。`split()`的第二个参数可以指定数组的大小，以便确保返回的数组不会超过既定大小。

***

# 单体内置对象： Other properties of the Global object
定义：由ECMAScript实现提供的、不依赖于宿主环境的对象，这些对象在ECMAScript程序执行之前就已经存在了。它们已经提前实例化了。

## Global

1. URI编码方法
  - `encodeURI()`：用于整个URI
  - `encodeURIComponent()`：主要用于encode URI的某一段。使用这个方法的情形更多
  - `decodeURI()`
  - `decodeURIComponent()`
2. eval()
3. window对象

## Global对象的属性
  - undefined
  - NaN
  - Infinity
  - Object
  - Array
  - Function
  - Boolean
  - String
  - Number
  - Date
  - RegExp
  - Error
  - EvalError
  - RangeError
  - ReferenceError
  - SyntaxError
  - TypeError
  - URIError

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

***

# Keyed collections

## Map
[ECMA-262 6th edition - Map](http://www.ecma-international.org/ecma-262/6.0/#sec-map-constructor)

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
