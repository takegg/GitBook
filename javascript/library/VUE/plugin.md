# plugin

## 目录结构

```
.
+--src                              # 项目源码
|  +--plugins                       # 自定义插件目录
|  |  +--pluginExample              # 自定义插件包
|  |  |  +--index.js                # 插件注册文件
|  |  |  +--pluginExample.vue        # 插件文件,类似组件写法
|  +--views                         #视图
|  |  +--example.vue
```

pluginExample.vue
```js
<template>
    <div>
    {{property}}
    </div>
</template>

<script>
    export default{
        name:'pluginExample',
        props:['property']
    }
</script>

<style>
</style>
```

index.js
```js
import pluginComponent from './pluginExample.vue';

let $vm;
const plugin = {
    install(vue, options) {
        const pluginExample = vue.extend(pluginComponent);
        if (!$vm) {
            $vm = new pluginExample({
                el: document.createElement('div')
            });
            document.body.appendChild($vm.$el);
        }
        const pluginExample = {
            fn1() {
                $vm.property = 1;
            },
            fn2() {
                $vm.property = 2;
            }
        };
        vue.$pluginExample = pluginExample;
        vue.prototype.$pluginExample = pluginExample;
    }
};

export default plugin;
```

example.vue
```html
<script>
import Vue from 'vue'
Vue.$pluginExample.fn1();
</script>
```

### 资源
<a href="https://juejin.im/post/58d9aae02f301e007e8ee278">Vue.js 插件开发详解</a>
<a href="https://www.cnblogs.com/luozhihao/p/7414419.html">vue插件编写与实战</a>