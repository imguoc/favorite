every

语法

arr.every( callback ( 元素值，元素的索引，原数组 ) ) | 返回 Boolean

检测数组的 `所有` 项是否满足条件，都满足返回 `true`，否则返回 `false`

相当于：条件1 && 条件2 && 条件3

``` js

var ifList = [
	{
		name: '条件1',
		required: true,
	},
	{
		name: '条件2',
		required: true,
	},
	{
		name: '条件3',
		required: true,
	},
]

var result = ifList.every(item => {
    return item.required
})

console.log(result)
// true

```