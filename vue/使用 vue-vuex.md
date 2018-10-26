使用 vuex

[vue-vuex 官方文档](https://vuex.vuejs.org/zh/)

安装

vue-cli 2.x  `npm install vue-vuex --save`

vue-cli 3.x  `vue add vuex`

目录

```
|-- ~/
|-- store
    |-- globalData
        |- index.js
    |-- index.js
|-- main.js
|-- ~
```

/main.js
```js
import App from './App.vue'
import store from './store'

// ...

new Vue({
    store,
    render: h => h(App)
}).$mount('#app')
```

/store/index.js
```js
import Vue from 'vue'
import Vuex from 'vuex'

import globalData from './globalData'

Vue.use(Vuex)

const store = new Vuex.Store({
    state = {}
    getters = {}
    mutations = {}
    actions = {}
    modules = {
        globalData
    },
    strict: process.env.NODE_ENV !== 'production'
    // 严格模式，禁止在生产环境时使用
})

export default store
```

/store/globalData/index.js
```js
const state = {
    count: 0
}

const getters = {
    sumCount: state => {
        return state.count + 100
    }
}

const mutations = {
    addCount (state, payload) {
        state.count += payload
    },
    subtractCount (state, payload) {
        state.count -= payload
    }
}

const actions = {
    addCountAction ({commit}, payload) {
        commit('addCount', payload)
    },
    subtractCountAction ({commit}, payload) {
        commit('subtractCount', payload)
    },
    // addCountAction (state, payload) {
    //     state.commit('addCount', payload)
    // },
    // subtractCountAction (state, payload) {
    //     state.commit('subtractCount', payload)
    // },
}

export default {
    state,
    getters,
    mutations,
    actions,
    namespaced: true
}
```

组件使用 state：`state` 是全局共享的变量
```js
<template>
    <div> 
        {{ count }} 
    </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
    computed: {
        ...mapState('globalData', [
            'count'
        ])
        // ...mapState('globalData', {
        //   count: state => state.count
        // })
    },
}
</script>
```

组件使用 getters：`getters` 相当于 `state` 的计算属相
```js
<template>
    <div> 
        {{ sumCount }} 
    </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
    computed: {
        ...mapGetters('globalData', [
            'sumCount'
        ]),
        // ...mapGetters('globalData', {
        //   sumCount: 'sumCount'
        // })
    },
}
</script>
```

组件使用 mutations：`mutations` 是同步改变 `state` 的方法
```js
<template>
    <div> 
        {{ count }}
        <button @click="addCount(10)">BTN+</button>
        <button @click="subtractCount(10)">BTN-</button>
    </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex'

export default {
    computed: {
        ...mapState('globalData', [
            'count'
        ])
        // ...mapState('globalData', {
        //   count: state => state.count
        // })
    },
    methods: {
        ...mapMutations('globalData', [
            'addCount',
            'subtractCount'
        ]),
        // ...mapMutations('globalData', {
        //     add: 'addCount',
        //     subtract: 'subtractCount'
        // }),
    }
}
</script>
```

组件使用 actions：`actions` 是异步改变 `state` 的方法
```js
<template>
    <div> 
        {{ count }}
        <button @click="addCountAction(10)">BTN+</button>
        <button @click="subtractCountAction(10)">BTN-</button>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState('globalData', [
            'count'
        ])
        // ...mapState('globalData', {
        //   count: state => state.count
        // })
    },
    methods: {
        ...mapActions('globalData', [
            'addCountActions',
            'subtractCountActions'
        ]),
        // ...mapActions('globalData', {
        //     addAction: 'addCountActions',
        //     subtractAction: 'subtractCountActions'
        // }),
    }
}
</script>
```

[其他参考 - 最详细的Vuex教程](https://blog.csdn.net/h5_queenstyle12/article/details/75386359)