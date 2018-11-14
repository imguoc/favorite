find

语法

arr.map( callback( 元素值，元素的索引，原数组 ) ) | 返回符合条件的第一项

检测当前项是否满足条件，满足添加直接返回当前项；没有满足条件的最后返回 undefined。不改变原数组

``` js

var arr = [
    {
        id: '001',
        name: 'item1',
    },
    {
        id: '002',
        name: 'item2',
    },
    {
        id: '003',
        name: 'item3',
    },
]

console.log(arr.find(item => item.name === 'item1').id)
// 001

```