# vuex

### 目录结构

```
.
+--src
|  +--store
|  |  +--modules
|  |  |  +--exampleMoudules.js
|  |  +--index.js
|  |  +--mutationType.js
|  +--views                         #视图
|  |  +--example.vue
```

index.js
```js
import Vue from 'vue'
import Vuex from 'vuex'
import actions from './actions'
import getters from './getters'
import exampleMoudules from './modules/exampleMoudules.js' //其中一个模块
......
import createPersistedState from 'vuex-persistedstate' //state持久化插件

Vue.use(Vuex)

export default new Vuex.Store({
  namespaced:true,//使用actions,getters,mutations时需加模块名
  modules:{
      exampleMoudules,// 该模块包含自己的state,actions,getters,mutations,
      ......
  },
  strict: false, // 因为使用了store.replaceState，所以这里关闭store检查
  plugins: [createPersistedState(),debug?createLogger():null]
})

```

mutationType.js
```js
//一个模块 
export const SET_EXAMPLE = 'SET_EXAMPLE' // 显示/设置数据
```

exampleMoudules.js
```js
import {
    SET_EXAMPLE,
} from '../mutationTypes';

import ajaxService from '@services/example.js'

const state = {
    filed:"" // 共享的数据
}

// 操作状态，为同步函数
const mutations = {
    [SET_EXAMPLE](state, exampleData) {
        state.filed += exampleData;
    },
}

// 定义网络请求动作，为异步函数
const actions = {
    set_example_action({commit, state}, req) {
        ajaxService.ApiMoudule({
            params:''
        }).then(data => {
            transformData(data);//自定义对数据处理
            commit(SET_EXAMPLE, data);//触发相应mutation
        });
    }
}

// 获取字段值
const getters = {
    getFiled: state => state.filed,
}

export default {
    state,
    actions,
    mutations,
    getters
};
```

example.vue
```js
<template>
    <div @click = "customeAsyncFn()">{{filed}}</div>
    <div @click = "customeFn()">{{filed}}</div>
</template>

<script>
import {mapActions,mapGetters,mapMutations} from 'vuex';
    export default {
        data(){
            filed:'',
        },
        methods:{
            ...mapActions({ // 异步函数
                customeAsyncFn:'set_example_action'
            }),
            // this.$store.dispatch(actionName) 直接触发
            ...mapMutations({ // 同步函数
                customeFn:'SET_EXAMPLE' // 映射 `this.customeFn()` 到 `this.$store.commit('SET_EXAMPLE')`
            })
            // this.$store.commit('mutationName') 直接触发
        },
        computed:{
            ...mapGetters({
                filed:getFiled
            }),
        }
    }
</script>
```