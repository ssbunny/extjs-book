# 类系统

JavaScript 是一门富有表现力的编程语言，它既可以进行面向对象编程(OOP)，
也可以进行函数式编程(FP)。函数是 JavaScript 的一等公民。
面向对象编程风格相对要简单许多，这也是 ExtJS 的选择。

## 传统方式
我们先来看一下传统的使用 JavaScript 实现 OOP 的代码：

```js
var Programmer = function (config) {
    this.name = config.name || '';
    this.lang = config.lang || '';
};

Programmer.prototype = {
    program: function () {
        console.log(this.name + ' codes in ' + this.lang + '.');
    }
};
```

我们借用函数对象模拟出“类“的概念，并创建了 `Programmer` 类。同时，
给此类增加了两个属性： `name` 和 `lang` 。紧接着，我们在 Programmer
的原型对象上增加了 `program` 方法(函数对象的属性与原型对象的属性是有区别的，
但不在本教程的讨论范围)。


