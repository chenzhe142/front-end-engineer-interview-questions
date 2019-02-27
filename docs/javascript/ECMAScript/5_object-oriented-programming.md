# Object-oriented programming

## 理解object

### 数据属性

类型：

- `[[Configurable]]`：能否通过delete删除属性，从而重新定义属性。一旦设置为`configuarble: false`，便不能再改变。
- `[[Enumerable]]`：表示能否通过`for-in`循环返回属性
- `[[Writable]]`：表示能否修改属性的值
- `[[Value]]`：包含这个属性的数据值

要修改属性默认的特性，必须使用`Object,defineProperty()`方法(Available since ECMAScript 5)。这个方法接收三个参数：属性所在的对象，属性的名字，一个描述符对象(descriptor: `configurable`, `enumerable`, `writable`, `value`).

在使用`Object,defineProperty()`时，如果不specify某些值，它们会默认为`false`。

```javascript
const person = {
  name: 'hamachi',
};

Object.defineProperty(person, 'name', {
  value: 'maguro',
});
```

### 访问器
访问器类似于一个指向其他数据的指针，不存在自己的value，而是指向其他的object。

**访问器属性不包含数据值**（没有`[[Value]]`），包含`getter`和`setter`函数。
- 在读取访问器属性时，会调用`getter`函数，这个函数负责返回有效的值。
- 在写入访问器属性时，会调用`setter`函数，这个函数负责决定如何处理数据

类型：

- `[[Configurable]]`：能否通过delete删除属性，从而重新定义属性，能否修改属性的特性，或者能否把属性修改为数据属性。一旦设置为`configuarble: false`，便不能再改变。
- `[[Enumerable]]`：表示能否通过`for-in`循环返回属性
- `[[Get]]`：在读取属性时调用的函数。默认值为`undefined。`
- `[[Set]]`：在写入属性时调用的函数。默认值为`undefined。`

不一定非要同时指定`getter`和`setter`。只指定`getter`意味着属性是不能写，尝试写入属性会被忽略。

访问器属性不能直接定义，必须使用`Object,defineProperty()`方法。

```javascript
const book = {
  _year: 2004,
  edition: 1,
};

Object.defineProperty(book, 'year', {
  get: function() {
    return this._year;
  },
  set: function(newVal) {
    if (newVal > 2004) {
      this._year = newVal;
      this.edition += newVal - 2004;
    }
  }
});
```

### 定义多个属性
```javascript
Object.defineProperties(book, {
  name: {
    value: 'genji'
  }
});
```

### 读取属性的特性
```javascript
Object.getOwnPropertyDescriptor(object, property);
```

## 创建object

### factory

### constructor:
使用`Person.call(newPerson, 'chris', 25)`。
问题：每个function都需要在每个instance重新创建。

### prototype

1. 理解prototype
`prototype`最开始只包含`constructor`属性。

虽然使用object instance可以访问prototype中的function，但不能通过object instance来修改。
```javascript
function Person() {
}

Person.prototype.name = 'adam';

const person1 = new Person();
person1.name = 'blake';

console.log(person1.name); // => 'black'
```

`blake`这个值存在于person1这个实例中。当试图访问`person1.name`时，需要读取它的值，因此就会在这个实例上搜索一个名为`name`的属性。这个属性确实存在，于是就返回它的值，而不必搜索prototype了。

当为对象实例添加一个属性时，这个属性就会屏蔽prototype中的同名属性，而不是覆盖prototype chain上的属性。

2. prototype和`in`操作符

**在单独使用时，`in`操作符会在通过对象能够访问给定属性时返回true（无论该属性存在于实例中还是原型中）。**

**在使用`for-in`循环时，，返回的是所有能够通过对象访问的、可枚举的(enumerable)属性，其中既包括存在于实例中的属性，也包括存在于prototype的属性。**


因此，当`in`操作符返回true，且`hasOwnProperty()`返回false时，可以确定属性存在于prototype中。


3. 方法
- `Object.defineProperty`
- `Object.prototype.hasOwnProperty()`：检测一个属性是存在于实例中，还是存在于prototype中。它只在给定存在于object instance中时，才会返回`true`
- `Object.prototype.isPrototypeOf`
- `Object.keys()`：取得对象上所有可枚举的实例属性
- `Object.getOwnPropertyNames()`：取得对象上的所有属性，无论是否enumerable
- `Object.getOwnPropertyDescriptor()`
