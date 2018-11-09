promise 解决回调地狱

语法
```js
new Promise( function(resolve, reject){
    // ...
    // 一般都是异步请求
    // ...
    if (true) {
        let result
        // ...
        resolve(result)
    } else {
        let err
        // ...
        reject(err)
    }
}).then(res => {
    let result
    // ...
    return result
}).then(res => {
    // ...
}).catch(err => {
    // ...
})
```

实例方法

Promise.prototype.then()

Promise.prototype.catch()

Promise.prototype.finally()

```js
let foo = new Promise((resolve, reject) => {
    if (条件语句) {
        return resolve(response)
    } else {
        reject(error)
    }
})

foo.then(res => {
    处理成功逻辑
}).catch(err => {
    处理异常逻辑
}).finally(() => {
    成功异常都会执行
})
```

静态方法

Promise.all()

```js
let foo = new Promise(···)
let bar = new Promise(···)

Promise.all([foo, bar]).then(result => {
    当 foo 和 bar 都返回成功时调用。result为数组，[foo的resolve, bar的resolve]
})
```

Promise.race()

Promise.reject()

Promise.resolve()

[Promise - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#语法)

[我对Promises的理解 - 简书](https://www.jianshu.com/p/b497eab58ed7)