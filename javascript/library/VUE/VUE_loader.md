# VUE_loader

用此脚手架需根据项目做修改

## 安装并配置插件

#### scss

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

#### 安装并配置axios
1. 安装
  ```bash
  $ npm install axios --save
  ```
2. 配置
    在src下新建services/index.js，
  ```
  ```
#### 安装vuex
  ```bash
  $ npm install vuex --save
  ```
  配置vuex
  ```
  ```

## 配置路由
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
+--static                           # 项目静态资源
```

