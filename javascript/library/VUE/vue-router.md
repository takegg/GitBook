# vue-router

```
+--src
|  +--router
|  |  +--index.js
|  |  +--map
|  |  |  +--example_router.js
|  +--views
|  |  +--example_module
|  |  |  +--example.vue
```

index.js
```js
import Vue from 'vue';
import Router from 'vue-router';

// 加载不同路由模块
import Example_router_module from './map/example_router'; //example_router模块

Vue.use(Router);

const router = new Router({
    mode:'',//模式
    routes: [
        ...Example_router_module,
    ]
});

router.beforeEach((to, from, next) => {//路由跳转前拦截
// 权限校验
});
router.afterEach((to, from, next) => {//路由跳转后拦截
    document.title = to.meta.title;//页面标题
});

export default router;
```

example_router.js
```js
const example = () => import('views/example_module/example');//example.vue文件省略.vue

export default [
    { name: 'example', path: '/example', component: example, meta: {title: '标题'} },
];
```