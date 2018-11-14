# VUE_loader

用此脚手架需根据项目做修改

## 安装并配置插件

#### 安装并配置scss

```shell 
$ npm install node-sass --save-dev
$ npm install sass-loader --save-dev
````

修改webpack.base.config.js,在module里的rules中加上。 **无单独.scss文件不用加**
```js
  {
    test: /\.scss$/,
    loaders: ["style", "css", "sass"]
  }
```

#### 1. 安装并配置axios

  安装
  ```bash
  $ npm install axios --save
  ```
    
  配置

  在src下新建services/index.js，
  ```
  ```

#### 2. 安装vuex
  ```bash
  $ npm install vuex --save
  ```
  配置vuex
  ```
  ```

#### 3. 配置路由vue-router
  ```bash
  ```

## 环境变量

1. 安装cross-env
    ```bash
    $ npm install --save-dev cross-env
    ```
2. 设置多打包环境
    在config中新建env.config.js
    ```
    `use strict`
    module.exports = {
      DEV_ENV:{
        'ENV':'developement',
        'BASE_API':'ajaxURL',
        'OTHER_URL':'URL'
      },
      TEST_ENV:{
        DEV_ENV:{
          'ENV':'test',
        'BASE_API':'ajaxURL',
        'OTHER_URL':'URL'
        },
      PROD_ENV:{
        DEV_ENV:{
          'ENV':'product',
        'BASE_API':'ajaxURL',
        'OTHER_URL':'URL'
        },
      }
    }
    ```
    
    > 在webpack.base.conf.js和webpack.dev.conf.js分别引入自定义环境变量：
    > ```
    > const envConfigs = require('../config/env.config');
    > ```
    > 并在plugins:[{}]中添加：
    > ```
    > 'PROJECT_ENV': JSON.stringify(envConfigs[process.env.PROJECT_ENV])
    > ```
    > 其中 **PROJECT_ENV**是在package.js中通过cross-env定义的的环境变量

3. 在package.js的scripts中设置快捷命令,这些命令可以相互嵌套。
    ```bash
    'dev:D':   "cross-env PROJECT_ENV=DEV_ENV webpack-dev-server --line --progress --config build/webpack.dev.conf.js",
    'dev:T':   "cross-env PROJECT_ENV=TEST_ENV webpack-dev-server --line --progress --config build/webpack.dev.conf.js",
    'dev:P':   "cross-env PROJECT_ENV=PROD_ENV webpack-dev-server --line --progress --config build/webpack.dev.conf.js",
    'build:D': "cross-env PROJECT_ENV=DEV_ENV node build/build.js",
    'build:T': "cross-env PROJECT_ENV=TEST_ENV node build/build.js",
    'build:P': "cross-env PROJECT_ENV=PROD_ENV node build/build.js",
    ```
    > dev:启动本地服务，用于开发。
    > build：生成打包文件，用于投入服务器。
    > 根据需求定义。也可以定义一个dll.js来囊括所有插件包。


4. 在需要根据不同环境打包引用不同值(如，url，appId......等)的文件中引入 **全局变量PROJECT_ENV**


## 目录结构

```
.
+--build                            # webpack打包、本地服务配置
|  +--build.js                      # webpack打包
|  +--webpack.base.conf             # webpack本地服务 -基础
|  +--webpack.dev.conf.js           # webpack本地服务 -开发
|  +--webpack.prod.conf.js          # webpack本地服务 -生产
+--config                           # 环境变量配置
|  +--index.js
|  +--env.config.js                 # 多环境配置
+--src                              # 项目源码
|  +--app.js                        # 打包入口文件
|  +--services                      # 网络请求
|  |  +--index.js
|  |  +--example.js
|  +--views                         #视图
|  |  +--example.vue
|  +--assets                        # 项目线上静态资源
|  |  +--style
|  |  +--js
|  |  +--picture
|  |  +--front
|  +--store                        # vuex状态控制模块
|  |  +--modules
|  |  |  +--exampleMoudules.js
|  |  +--index.js
|  |  +--mutationType.js
+--static                           # 项目非线上静态资源
```

### 全局引入
app.js
```js
<!-- 常规引入 -->
import Vue from 'vue'
import App from './App'
import router from './router'
import store from './store'


import {Plugin1,Plugin2} from '~@/plugins/'
<!-- 还可引入公共css,js等 -->
Vue.use(Plugin1)
Vue.use(Plugin2)

new Vue({
  el: '#app',
  store,
  router,
  template: '<App/>',
})

```

### .VUE文件
```html
<template>
  <div></div>
</template>

<script>
import {}from'@/xxx'
export default{
  data(){
    return{
      xxx:""
    }
  },
  computed(){

  },
  beforeCreate(){

  },
  created() {},
  beforeMount() {},
  mounted(){

  },
  directives:{
    xxx:{
      bind:(el, binding, vnode)=>{}
    }
  },
  methods:{
    initData () {}
  },
  filters:{
    xxx(value){

    }
  },
  watch:{
    xxx:{
      handler (value, oldValue) {}
    }
  }
}
</script>

<style lang="scss" scoped></style>
```