# vue-cookie

[使用vue-cookies操作cookie](https://www.jianshu.com/p/60c13168cc8f)

```jsx
npm install vue-cookies --save
```

```jsx
import VueCookies from 'vue-cookies'
Vue.use(VueCookies)
```

main.js引入

```jsx
main.js

import VueCookies from 'vue-cookies'

app.config.globalProperties.cookies = VueCookies
```

组合式api 使用

```jsx
import {  getCurrentInstance} from 'vue';
const { proxy } = getCurrentInstance();
proxy.cookies.get('token')//获取
proxy.cookies.set('token',key),//添加
proxy.cookies.isKey('token')//查看是否有这个键值
proxy.cookies.remove('token')//删除

```