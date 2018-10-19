map

语法

arr.map( callback( 元素值，元素的索引，原数组 ) ) | 返回 Array

为每一项执行一次函数，并把返回值组合成新数组返回。不改变原数组

``` js

var arr = [1, 2, 3, 4, 5] 

var newArr = arr.map(v => {
	return v * 10
})

console.log(newArr)
// [10, 20, 30, 40, 50]

```