Object.assign

合并对象

语法：`Object.assign(目标对象， 参数对象)`

```js
const foo = {
    a: 1,
    b: 2,
    c: 3
}

const obj = Object.assign({}, foo)
```

参数对象里的属性会覆盖目标对象里的属相

如果参数对象指向一个引用，那 `assgin` 合并的对象是参数对象的浅拷贝
