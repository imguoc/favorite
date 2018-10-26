使用 router

[vue-router 官方文档](https://router.vuejs.org/zh/)

安装

vue-cli 2.x  `npm install vue-router --save`

vue-cli 3.x  `vue add router`

目录

```
|-- ~/
|-- router
    |-- news
        |- index.js
    |-- product
        |-- index.js
    |-- index.js
|-- main.js
|-- ~
```

/main.js
```js
import App from './App.vue'
import router from './router'

// ...

new Vue({
    router,
    render: h => h(App)
}).$mount('#app')
```

/router/index.js
```js
import Vue from 'vue'
import Router from 'vue-router'

import News from './news'
import Product from './product'

Vue.use(Router)

// 全局导航守卫
let whiteList = ['/login', '/404']
let TOKEN = true
router.beforeEach((to, from, next) => {
    if (whiteList.includes(to.path)) {
        next()
    } else if (!TOKEN) {
        next({path: '/404'})
    } else {
        next()
    }
})

const router = new Router([
    routes: [
        ...News,
        ...Product
    ]
])

export default router
```

/router/news/index.js

```js
import News from '@/views/news'

export default [
    {
        path: '/news',
        name: 'news',
        component: News
    }
]
```

路由懒加载 - 在访问的时候加载组件

修改 router/news/index.js

```js
// import News from '@/views/news'
const News () => improt('@/views/news')

export default [
    {
        path: '/news',
        name: 'news',
        component: News
    }
]
```
[其他参考：vue中的懒加载和按需加载](https://www.jianshu.com/p/b323dadfeda9)