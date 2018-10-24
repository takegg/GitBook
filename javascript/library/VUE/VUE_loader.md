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

### 环境变量

