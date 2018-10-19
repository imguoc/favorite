reduce

语法

arr.map( callback( 元素值，元素的索引，原数组 ), 初始值 ) | 返回指定累加数据

为每一项执行一次函数，并把返回值叠加到下一项回调函数。

``` js

// 按 sex 重新分组
var arr = [
    {
        sex: 'man',
        name: '小明',
    },
    {
        sex: 'woman',
        name: '小红',
    },
    {
        sex: 'woman',
        name: '小莉',
    },
    {
        sex: 'man',
        name: '小张',
    },
]

var newArr = arr.reduce((acc, item) => {
    var findItem = acc.find(v => v.sex === item.sex)
    if (findItem) {
        findItem.list.push(item)
    } else {
        acc.push({
            sex: item.sex,
            list: [item]
        })
    }
    return acc
}, [])

console.log(newArr)
// [
//     {
//         "sex": "man",
//         "list": [
//             {
//                 "sex": "man",
//                 "name": "小明"
//             },
//             {
//                 "sex": "man",
//                 "name": "小张"
//             }
//         ]
//     },
//     {
//         "sex": "woman",
//         "list": [
//             {
//                 "sex": "woman",
//                 "name": "小红"
//             },
//             {
//                 "sex": "woman",
//                 "name": "小莉"
//             }
//         ]
//     }
// ]

```