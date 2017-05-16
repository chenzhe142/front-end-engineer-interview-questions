# Object-oriented programming

## Understand object

### 属性类型

- `[[Configurable]]`：能否通过delete删除属性，从而重新定义属性
- `[[Enumerable]]`：表示能否通过`for-in`循环返回属性
- `[[Writable]]`：表示能否修改属性的值
- `[[Value]]`：包含这个属性的数据值

要修改属性默认的特性，必须使用`Object,defineProperty()`方法。这个方法接收三个参数：属性所在的对象，属性的名字，一个描述符对象(descriptor: `configurable`, `enumerable`, `writable`, `value`).
