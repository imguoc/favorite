promise 解决回调地狱

语法
```
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

方法

Promise.all()

原型方法

Promise.prototype.then()

Promise.prototype.catch()

Promise.prototype.finally()

[Promise - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#语法)