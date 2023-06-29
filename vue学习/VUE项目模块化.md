# VUE项目模块化

[](https://segmentfault.com/q/1010000006854993)

## Example

App,vue → app.js → data.js

data.js

```jsx
let datas = [{
    title: "hello world0"

}, {
    title: "hello world1"
}, {
    title: "hello world2"
}]

export default datas;
```

app.js

```jsx
import datas from './data'
let i = 0;

export default{
    
    data(){
        return{
            msg:datas[1].title
        }
    },
    mounted(){
        setInterval(()=>{
            if(i >= datas.length) i=0;
            this.msg = datas[i].title;
            i++
        },500)
    }
}
```

App.vue

在App.vue目录下新建js文件夹 → 新建app.js妈妈

```jsx
<template>
  <h1>{{msg}}</h1>
</template>

<script>
import app from './js/app'
export default{
  ...app
}

</script>
```