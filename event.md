# 事件模型

我们在使用 ExtJS 时，经常会为某组件绑定事件，以做相应扩展处理。
创建组件时通过配置 `listeners` 属性即可绑定事件：

```js
var i = 0;
var btn = Ext.create('Ext.button.Button', {
	text: 'Button',
	listeners: {
		mouseover: function (btn) {
			console.log(btn.getText() + ++i);
		}
	},
	renderTo: document.body
});
```

也可以通过 `on` 方法给组件实例绑定事件：

```js
btn.on('click', function () {
	alert('clicked');
});
```

以上方法已经能解决我们使用 ExtJS 事件时绝大多数需求。
然而当我们扩展或自定义一个组件时，常常需要注册自定义的事件并在合适的时机触发它们。
这一章要讲的事件模型分为三部分，以上为其一 ———— 绑定：

* 注册
* 触发
* 绑定





