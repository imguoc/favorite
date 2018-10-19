map

语法

arr.forEach( callback( 元素值，元素的索引，原数组 ) ) | 返回 undefined

为每一项执行一次函数，返回 undefined。

``` js

var arr = [1, 2, 3, 4, 5] 

var newArr = []
arr.forEach(v => {
	newArr.push(v * 10)
})

console.log(newArr)
// [10, 20, 30, 40, 50]

```