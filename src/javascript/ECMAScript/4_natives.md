# Natives: 基本包装类型

常用的原生对象有：String()，Number()，Boolean()，Array()，Object()，Function()，RegExp()，Date()，Error()，Symbol()。

可以看出，这些原生对象其实是内置函数。

## Internal [[Class]]

typeof结果为object的值额外有个[[Class]]属性来标记（可看做内部分类）。这个属性无法直接访问，可通过Object.prototype.toString(..)获取。

而对基础类型的值来说：

```javascript
Object.prototype.toString.call( null );         // "[object Null]"
Object.prototype.toString.call( undefined );    // "[object Undefined]"

Object.prototype.toString.call( "abc" );    // "[object String]"
Object.prototype.toString.call( 42 );       // "[object Number]"
Object.prototype.toString.call( true );     // "[object Boolean]"
```

对null和undefined来说，尽管没有Null()和Undefined()，但内部[[Class]]的值暴露了"Null"和"Undefined"。
对其它基础类型来说，输出的是它对应包装对象的[[Class]]。

***

## 包装对象的陷阱（Object Wrapper Gotchas）

```javascript
!new Boolean( false ); // false
typeof new String('a'); // object 注意，String前需要new
Object('a') instanceof String; // true 注意，Object前的new可以省略
```

## Boxing wrappers

### 拆箱（Unboxing）

使用valueOf()来获取包装对象对应的基础类型值。

```javascript
new String( "abc" ).valueOf() // "abc"
```

另外拆箱可以隐式发生，如new String( "abc" ) + ''。这个（类型转换）会在第四章讲。

## Natives as constructors
对于`array`，`object`，`function`，和正则来说，更常用的是它们的字面值形式。

就像上面看到的其它原生对象，这些构造函数形式一般要避免，因为构造函数可能带来陷阱。

### Native Prototypes

内置原生对象构造函数都有自己的.prototype对象。这些.prototype对象包含原生对象独特的行为。
