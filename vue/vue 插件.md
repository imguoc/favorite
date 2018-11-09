vue 插件

Vue 插件的种类：
* `Vue` 添加全局属性和方法（静态属性和方法）
* `Vue` 添加实例属性和方法
* `Vue` 添加全局资源，指令 `directives`，过滤器 `filters`，组件 `components`
* 通过全局 `mixin` 方法添加一些组件选项
* 一个库，提供自己的 `API`，同时提供上面提到的一个或多个功能

Vue 插件开发要点：
* 如果插件是一个对象，必须指定名为 `install` 的属性方法
* 如果插件是一个方法，会被作为 `install` 方法
* 插件必须在 `Vue` 实例化之前调用 `Vue.use()`
* `install` 方法会把 `Vue` 作为第一个参数传入，另外提供一个可选参数 `options`
* `install` 在插件内部，只会被调用一次
* 在通过 `script` 引入 `Vue` 时，Vue 会被作为全局对象。此时插件应在插件内部调用 `install`

/plugin/index.js
```js
const myPlugin = {}
myPlugin.install = function () {
    // ...
}

export default myPlugin

// const install = function () {
//     // ...
// }
// export default install

// Vue 作为全局对象时自动调用（script 方式引用 Vue）
if (typeof window !== 'undefined' && window.Vue) {
  window.Vue.use(myPlugin)
}
```

/main.js
```js
// ...
import Vue from 'vue'
import Plugin from './plugin'

Vue.use(Plugin) // 在实例初始化之前调用插件

new Vue({
    // ...
})
// ...
```

[其他参考 - Vue插件开发入门](https://www.cnblogs.com/libin-1/p/6254390.html)

[其他参考 - vue插件编写与实战](https://www.cnblogs.com/luozhihao/p/7414419.html)
