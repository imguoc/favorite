filter

语法

arr.filter( callback( 元素值，元素的索引，原数组 ) ) | 返回 Array

为每一项执行一次函数，并把符合条件的返回值组合成新数组返回。不改变原数组

``` js

var arr = [1, 2, 3, 4, 5]

var newArr = arr.filter(v => {
	return v >= 3
})

console.log(newArr)
// [3, 4, 5]

```