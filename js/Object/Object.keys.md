Object.keys

返回一个对象的属性名组成的数组

语法： `Object.keys(obj)`

```js
// 一个对象转数组的例子
const obj = {
    a: 1,
    b: 2,
    c: 3
}

let objToArr = function(obj) {
    return Object.keys(obj).reduce((acc, item, index) => {
        acc.push({
            key: item,
            value: obj[item]
        })
        return acc
    }, [])
}
```