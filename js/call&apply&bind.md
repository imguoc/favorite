`call`、`apply`、`bind` 都是重新指定上下文 `this` 的方法

`call` 和 `apply` 方法的作用类似。区别在于 `call` 参数是一个一个传， `apply` 参数可直接接受一个数组

`bind` 会执行一个新的函数，使用时要加上 `()` 调用方法


在非严格模式下，指定上下文 `this` 的值为 `null` 和 `undefined` 会自动指向全局上下文 `this`

`call` 语法：`fun.call(thisArg, arg1, arg2, ...)`

`apply` 语法：`func.apply(thisArg, [argsArray])`

```js
"use strict"

var foo = {
	name: 'name => foo',
	getName: function() {
		console.log(this.name)
	}
}

// getName 默认的上下文 this 是 foo
foo.getName() // name => foo

window.name = 'name => window'
// 把 getName 方法的上下文 this 指定到 window 
foo.getName.call(window) // name => window
foo.getName.apply(window) // name => window
foo.getName.bind(window)() // name => window

var bar = {
    name: 'name => bar'
}
// 把 getName 方法的上下文 this 指定到 bar 
foo.getName.call(bar) // name => bar
foo.getName.apply(bar) // name => bar
foo.getName.bind(bar)() // name => bar
```

其他参考：
[JavaScript 中 call()、apply()、bind() 的用法](http://www.runoob.com/w3cnote/js-call-apply-bind.html)