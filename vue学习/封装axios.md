# 封装axios

`useAxios` 是一个封装了 `axios` 的工具，提供了 `get` 和 `post` 方法，用于处理 API 调用并处理响应。使用 `axios` 的一个优点是可以处理异步操作，并使用 Promise 语法进行操作。使用 `useAxios` 的方法很简单，只需导入并调用其方法即可。本示例展示了如何使用 `useAxios.get` 方法以及在 Vue 组件中如何使用。通过封装 `axios`，可以更方便地进行 API 调用，同时还可以在多个文件中使用相同的代码，提高代码的可重复性和可维护性。

```jsx
import axios from 'axios';

const useAxios = {
    get(url,callback){
        return new Promise((resolve,reject)=>{
            axios
                .get(url)
                .then((res)=> callback ? callback(resolve(res.data)) : resolve(res.data) )
                .catch((err)=>{
                    reject(err)
                })
        })
        
    },
    post(url,params,callback){
        return new Promise((resolve,reject)=>{
            axios
                .post(url,{params})
                .then((res)=> callback ? callback(resolve(res.data)) : resolve(res.data) )
                .catch(err=>reject(err))
        })
    }
}

export default useAxios
```

使用

```jsx
import useAxios  from '../hooks/useaxios'

useAxios.get('http://192.168.3.123:3000/test')
    .then((res)=>{
        console.log(res)
})

```

```jsx
onMounted(async()=>{
    let res = await useAxios.get('http://192.168.3.123:3000/test')
    console.log(res)//{code:200,msg:'get'}
})
```