# Object

***

`Object` is a reference type. By using `new` operator, it creates an instance of `Object` reference type.

```javascript
const person = new Object();
```

这行代码创建了`Object`的一个新instance，并把其存储在`person` variable中。使用的constructor是`Object`，它只为new instance定义了默认的property和function。

***

虽然Object instance不具备多少功能，但对于在application中存储和传输数据而言，它们确实是非常理想的选择

```
const person = {
  "name": 'adam',
  age: 3
};
```
在最后一个property后加`,`，会在IE7以及更早的版本和opera中导致错误。

***

```javascript
function getCar(brand, options = {}) {
  this.brand = brand;
  this.color = options.color || 'red';
}
```

在传递大量optional parameter的时候推荐用object包裹住，必要的parameter使用命名参数。
