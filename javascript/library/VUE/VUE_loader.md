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
```bash
$ npm install axios --save
```
配置axios
```
```
#### 安装并配置vuex
```bash
$ npm install vuex --save
```
配置vuex
```
```

#### 配置路由
```bash
```

### 环境变量

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
   > 其中 **PROJECT_ENV**是在package.js中引用的环境变量

   3. 在package.js的scripts中设置快捷命令
   ```bash
   'dev:D':"cross-env PROJECT_ENV=DEV_ENV webpack-dev-server --line --progress --config build/webpack.dev.conf.js",
   ```
   ......等，根据需求定义。也可以定义一个dll.js来囊括所有插件包。