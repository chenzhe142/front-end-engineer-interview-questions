# fundamentals

***

## 严格模式 strict mode: `use strict`
- ECMAScript 5引入了strict mode。它为javascript定义了一种不同的解析与执行模式。
- `use strict`是一个编译指示(pragma)，用于告诉支持的javascript引擎切换到strict mode。在function内部的上方包含这条编译指令，也可以指定function在strict mode下执行。
- 支持strict mode的浏览器有IE 10+, Firefox 4+, Safari 5.1+, Opera 12+和chrome.
- It disables `arguments` params. It changes the behavior of Javascript engines so that errors are thrown instead of silently picked up.

***

## variables
- 在省略`var`声明变量时，variable会变成global variable。不推荐这样做。在strict mode下会抛出ReferenceError。

***

## data type
### `typeof` operator
  - 使用`typeof`可以检测给定variable的数据类型。
  - `undefined`, `boolean`, `string`, `number`, `object`(这个variable是object或null), `function`

### `Undefined`类型
  - 对未声明和未初始化的variable使用typeof，均会返回undefined

### `Null`类型
  - 从逻辑上讲，`null`值表示一个空对象指针，而这也正是使用`typeof` operator检测`null`时返回`object`的原因。
  - 如果定义的variable在将来用于保存对象，那么最好将其initialize为`null`，而不是其他值。这样一来，只要直接检查`null`就可以知道相应的variable是否保存了一个object的reference。

### `Boolean`类型

| data type | true             | false |
| --------- | ---------------- | ----- |
| Boolean   | true             | false |
| String    | non-empty string | empty string |
| Number    | non-zero         | 0, NaN |
| Object    | object           | null |
| Undefined | N/A              | undefined |

### `Number`类型
  - Javscript用IEEE754格式来表示integer和floating points
  - 三种进制：
    - 十进制
    - 八进制: first number must be `0`
    - 十六进制: first two must be `0x`
  - 由于floating points需要的内存空间是integer的两倍，ECMAScript会不失时机地将floating points转换为integer
  - floating points的最高精度为17位小数，但在进行算术计算时其精确度远远不如整数。例如，0.1加0.2的结果不是0.3，而是0.30000000000000004。这个rounding误差会导致无法测试特定的floating points。这是使用IEEE754的通病。
  - 数值范围
    - `Number.MIN_VALUE`: `5e-324`
    - `Number.MAX_VALUE`: `1.7976931348623157e+308`
    - `Number.NEGATIVE_INFINITY`
    - `Number.POSITIVE_INFINITY`
    - 如果计算时的结果超出范围，结果会被转化为`-Infinity`或`Infinity`
  - `NaN`: not a number
    - 任何涉及`NaN`的操作都会返回`NaN`
    - `NaN`与任何值都不相等
    - function `isNaN()`会帮我们确定这个参数是否`不是数值`
    - 在对一个object使用`isNaN()`时，会首先调用`valueOf()`，然后确定该方法返回的值是否可以转化为数值。如果不能，则基于这个返回值再调用`toString()`方法，再测试返回值。
  - 数值转换
    - `Number()`
      1. if Boolean, true is 1, and false is 0.
      2. if Number, simply pass it
      3. if null, 0
      4. if undefined, return NaN
      5. if string:
        - if empty, return 0
        - if number, return a number
        - if not, return NaN
      6. if object:
        - call `valueOf()`
        - then call `toString()`
    - `parseInt()`
      - 会忽略string前的whitespace，直至第一个非whitespace字符
      - ECMAScript 5 JavaScript引擎已经不具备解析八进制值的能力。
      - 多数情况下，我们要parse的都是十进制数值，因此始终将10作为第二个参数是非常重要的。
    - `parseFloat()`
      - 字符串中第一个小数点是有效的
      - 只解析十进制的值

### `String`类型
  - 16位d的unicode characters
  - escape notation: will be treated as 1 character
  - **immutable**: 要改变某个变量保存的字符串，首先要销毁原来的字符串，再用另一个包含新值的字符串填充该变量。这个过程是在后台发生的。
  - 转换字符串
    - 使用`toString()`。string会返回一个copy
    - 当number调用此function时，可以传递一个parameter，进制数
    - `null`和`undefined`没有`toString()` function。
    - 在不知道要转换的值是不是null或undefined的情况下，还可以使用`String()`，这个函数能够将任何类型的值转换为string.
      - 如果有`toString()`方法，调用`toString()`
      - 如果是null, 返回`"null"`
      - if undefined, return `"undefined"`

### `Object`类型
`Object`的每个instance都有下列属性和方法，以下方法均位于`Object.prototype`上。
  1. `Constructor`
  2. `hasOwnProperty(propertyName)`: 用于检查给定property在当前的instance（而不是在prototype）中是否存在
  3. `isPrototypeOf(object)`: 用于检查传入的object是否为另一个对象的prototype
  4. `propertyIsEnumerable(propertyName)`: 用于检查给定property是否能够使用for-in语句。`propertyName`必须为string。
  5. `toLocalString()`
  6. `toString()`: 返回instance的字符串表示
  7. `valueOf()`: 通常与`toString()`的返回值相同

## operator
  - 一元operator：前置型，后置型 `++`, `--`
  - bitwise operator
    - signed integer: 第一位表示正负，剩下31位表值。第一位不能access
  - comparison operator
    - 在比较字符串时，实际比较的是两个字符串中对应位置的每个字符的字符编码值。大写字母的编码值全部小于小写字母。如果要按照真正的顺序比较字符串，需要转换成统一的大小写。
  - equals operator
    - 相等 & 不相等 `==`: 会主动转换成相似的类型，再进行比较
    - 全等 & 不全等 `===` **recommended**: 不转换类型，仅比较

***

## statements

### `if` statement
- [ ] add here

### `for-in` statement
- Object properties in ECMAScript is **unordered**. 通过`for-in` loop输出的propertyName的顺序是不可预测的。
- 如果要iterate的Object为null或undefined，for-in loop会throw error。ECMAScript 5更正了这一行为，不再抛出error，而是不执行loop

### `label` statement
- syntax: `label: statement`

```javascript
start:  for (let i = 0; i < count; i += 1) {
  alert(i);
}
```

- label `start` can be referenced later by `break` or `continue`
- 使用lable和break，可以实现break外层for-loop的情形。但要避免在很多nested loops中使用label，因为这样会增加debugging和阅读代码但难度。

### `with` statement
- it sets the scope of the code within a particular object.
- It is rarely used.

### `switch` statement
- works with **all data type**
- `switch` uses `===` instead of `==`
- it's best to put a `break` statement after each case to avoid having cases fall through into the next one.
- if you need a case statement to fall through, include a comment indicating.
  ```javascript
  switch (i) {
    case 1:
      /* falls through */
    case 2:
      alert('yaya');
      break;
    default:
      alert('sad');
  }
  ```

***

## Function
- **be consistent**: it is recommended that a function either always return a value or never return a value.
- `arguments` in ECMAScript are represented as an array internally. It acts like an array, however, it is not an instance of `Array`
- use `arguments.length` to know how many arguments are passed in.
- **named arguments are  a convenience, not a necessity**
- in strict mode, overriding argument will throw `SyntaxError`, and unpassed variables will remain `undefined` even though `argument` is assigned values.
- all arguments in ECMAScript are passed by value, not by reference.
- function overloading is not possible because of the lack of function signatures.
