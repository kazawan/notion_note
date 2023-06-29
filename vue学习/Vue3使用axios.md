# Vue3使用axios

[Vue 3.x 中使用 Axios 请求远程Api接口数据](https://www.cnblogs.com/qingheshiguang/p/14618614.html)

`MAIN.JS` 引入

```jsx
import Axios from 'axios'
app.config.globalProperties.Axios = Axios
```

### 攔截器

```jsx
const axios = require('axios')

// const instance = axios.create({
//     baseURL: 'https://api.example.com'
// });

const i = axios.create({
    baseURL: 'https://www.jianshu.com/p/2ac6c0198ad4',
    timeout: 5000
})

i.interceptors.request.use((config)=>{
    console.log(">>>",config.method )
    console.log(">>>",config.method )
    return config
},(err)=>{
    return Promise.reject(err)
})
i.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    console.log("<<<",response )
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  });

i.get().then((data)=>{
    data
})
```

### 传入headers

定义配置文件

```jsx
const axiosconfig = {
  headers: {
    'Content-Type': 'application/json',
    'authorization': proxy.cookies.get('token'),
    
  }
}
```

get与post方法得传入config文件

```jsx
axios.get(url,axiosconfig)
axios.post(url,{data},axiosconfig)
```