# vue 引入自己写得库

## 方法

- 生成一个js文件 “ help.js”

```
let help = 1;
export{
    help as default
}
```

- 在main.js 中引入

```jsx
import help from './assets/help'
app.config.globalProperties.help=help
```

[那么在APP.VUE或者组件中就用this.help](http://那么在APP.VUE或者组件中就用this.help) 这个变量

参考网站

[Vue 3.x 中使用 Axios 请求远程Api接口数据](https://www.cnblogs.com/qingheshiguang/p/14618614.html)