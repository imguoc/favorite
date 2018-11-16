vue 中的简单使用

安装

`npm install axios --save`

目录

```
|-- ~/
|-- api
    |-- login
        |- index.js
    |-- fetch.js
    |-- index.js
|-- main.js
|-- ~
```

设置开发环境跨域

修改文件 `config/index.js`文件下`dev`的配置`proxyTable`

```js
proxyTable: {
    '/api': {
        target: 'xxx', // 接口域名
        changeOrigin: true, // 是否跨域
        pathRewrite: {
        '^/api': ''   //重写接口
        }
    }
},
```

`fetch.js`是对`axios`的一个封装

```js
import axios from 'axios'

const instance = axios.create({
    // config
})

// 请求拦截器 
instance.interceptors.request.use(function (config) {
    // ...
    return config
}, function (error) {
    // ...
    return Promise.reject(error)
})

// 响应拦截器
instance.interceptors.response.use(function (response) {
    // ...
    return response
}, function (error) {
    // ...
    return Promise.reject(error)
})

export default instance
```

业务模块`login.js`

```js
import fetch from '@/api/fetch'

export function GetToken (param) {
    return fetch.post('/api/GetToken', param)
}
```

导出所有接口`api/index.js`

```js
export * from './login'
```

业务模块`login.vue`
```vue
// ...
<script>
import { GetToken } from '@/api'

expoot default {
    // ...
    methods: {
        login () {
            GetToken().then(res => {
                console.log(res)
            }).catch(err => {
                console.log(err)
            })
        }
    }
}
</script>
```
参考

[webpack之proxyTable设置跨域](https://www.cnblogs.com/wancheng7/p/8987694.html)

[Axios 中文说明](https://www.kancloud.cn/yunye/axios/234845)

[axios](https://github.com/axios/axios)