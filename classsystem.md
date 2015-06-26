# 类系统

JavaScript 是一门富有表现力的编程语言，它既可以进行面向对象编程(OOP)，
也可以进行函数式编程(FP)。函数是 JavaScript 的一等公民。
面向对象编程风格相对要简单许多，这也是 ExtJS 的选择。

## 传统方式
我们先来看一下传统的使用 JavaScript 实现 OOP 的代码：

```js
var Programmer = function () {
    this.lang = 'java';
    this.name = '';
};

Programmer.prototype = {
    isProgrammer: true,
    setName: function (name) {
        this.name = name;
    },
    program: function () {
        console.log(this.name + ' codes in ' + this.lang + '.');
    }
};
```

我们借用函数对象模拟出“类“的概念，并创建了 `Programmer` 类。同时，
给此类增加了两个属性： `name` 和 `lang` 。紧接着，我们在 Programmer
的原型对象上增加了 `isProgrammer` 属性和 `setName` 、`program` 方法
(函数对象的属性与原型对象的属性是有区别的，但不在本教程的讨论范围)。

现在来看看如何创建 `Programmer` 的实例并调用其方法：

```js
var zhangsan = new Programmer();
zhangsan.setName('ZhangSan');
if (zhangsan.isProgrammer) {
    zhangsan.program();
}
```

控制台将打印出：

```sh
ZhangSan codes in java.
```

这看上去并不难。那么如果我们想模拟出“子类”及“继承”的概念呢？
我想先给你看一下它的代码实现：

```js
var Geek = function () {
    Geek.superclass.constructor.call(this);
    this.niubility = true;
};
Geek.prototype = new Programmer();
Geek.superclass = Programmer.prototype;

Geek.prototype.superSkill = function () {
    return 'kill himself.';
};
```

我们实现了 `Programmer` 的子类 `Geek` 并为其扩展了 `niubility`
属性和 `superSkill` 方法。这里将 `Geek` 的原型指向 `Programmer`
的一个实例，以此来获得 `Programmer` 上的所有属性及方法。除此之外，
我们还将 `Geek` 的 `superclass` 指向 `Programmer.prototype` ，
这么一来便可以通过 `superclass` 引用调用并继承父类方法。

如果上面的代码对你来说并不容易理解，那么你可能需要补充一下 JavaScript
的相关知识。虽然 ExtJS 为我们隐藏了诸多实现细节，但若想有所提高并了解
ExtJS 的工作原理，准确理解以上代码是极为必要的。更多 JavaScript
面向对象编程的知识，我推荐你阅读
[MDN文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)

接下来构造一个 `Geek` 实例并调用其方法：

```js
var lisi = new Geek();
lisi.setName('LiSi');
lisi.lang = 'JavaScript';

if (lisi.isProgrammer && lisi.niubility) {
    lisi.program();
    console.log(lisi.name + ' can ' + lisi.superSkill());
}
```

控制台将打印出：

```sh
LiSi codes in JavaScript.
LiSi can kill himself.
```

## ExtJS的方式

从上一小节可以看出，传统的面向对象编程方式稍有些复杂，而且代码较为分散，
继承关系也不直观。ExtJS 为了克服此问题，在 4.0+ 版本中引入了全新的类系统。
让我们先来看看如何用 ExtJS 的方式实现上一节的例子：

```js

Ext.define('Programmer', {

    isProgrammer: true,

    constructor: function () {
        this.lang = 'java';
        this.name = '';
    },

    setName: function (name) {
        this.name = name;
    },

    program: function () {
        console.log(this.name + ' codes in ' + this.lang + '.');
    }
    
});

var zhangsan = Ext.create('Programmer');
zhangsan.setName('ZhangSan');
if (zhangsan.isProgrammer) {
    zhangsan.program();
}
```






