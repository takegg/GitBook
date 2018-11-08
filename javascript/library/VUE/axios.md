# axios

## 模块目录结构
```
+--services
|  +--index.js
|  +--example.js
+--views
|  +--example.vue
```
## 配置axios

index.js


```js
import axios from 'axios';
import Vue from 'vue';

const service = axios.create({
    timeout: 10000 // 请求超时时间
    <!-- withCredentials: true //是否要证书 -->
});

// 全局axios请求拦截处理
function reqBeforS (config) {
    Vue.$loading.show();
};
function reqBeforF (error) {
    Vue.$loading.hide();
};
function resBeforS (res) {
    Vue.$loading.show();
};
function resBeforF (err) {
  if (err && err.response) {
    switch (err.response.status) {
      case 400:
        err.message = '请求错误'
        break

      case 401:
        err.message = '未授权，请登录'
        break

      case 403:
        err.message = '拒绝访问'
        break

      case 404:
        err.message = `请求地址出错: ${err.response.config.url}`
        break

      case 408:
        err.message = '请求超时'
        break

      case 500:
        err.message = '服务器内部错误'
        break

      case 501:
        err.message = '服务未实现'
        break

      case 502:
        err.message = '网关错误'
        break

      case 503:
        err.message = '服务不可用'
        break

      case 504:
        err.message = '网关超时'
        break

      case 505:
        err.message = 'HTTP版本不受支持'
        break

      default:
    }
    if (error.config && error.config['requestId']) {
        clearTimeout(error.config['requestId']);
    }
    Vue.$loading.hide();
    // router.replace('/error');

  }
};


// 添加请求拦截器
service.interceptors.request.use(config => {// config为axios的API
    reqBeforS(config);
    return config;
}, error => {
    reqBeforFailed(error)
    Promise.reject(error);
});

// 添加响应拦截器
service.interceptors.response.use(response => {
    resBeforS(response)
    return response;
}, error => {
    resBeforF(error)
    return Promise.reject(error);
});

export default service;

```

### 按模块划分ajax
example.js
```js
import vajax from './index';

const projectEnv = PROJECT_ENV; //引入全部环境变量
const BaseAPI = projectEnv.BASE_API; //ajax请求前缀

const exampleGet = (option) => {
    return new Promise((resole,reject)=>{
        vajax({
            method:'get',
            url:`${BaseAPI}URLString`,
            responseType:'json',
            // data:body //应该是formData
        }).then(respones => {
            resolve(response.data);
        }).catch(error => {
            reject(error);
        })
    });
}

export default{
    exampleGet
}
```

### 调用API
example.vue
```js
<template>
    <div></div>
</template>

<script>
    import ajaxService from '@/services/example.js'

    export default {
        methods:{
            test(optionsObj){
                ajaxService.exampleGet(optionsObj).then(res=>{
                    console.log(res)
                }).catch(err)=>{
                    console.log(err)
                }
            }
        }
    }
</script>
```