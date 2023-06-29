# VUEX 使用

中文文檔

[Vuex 是什么？ | Vuex](https://vuex.vuejs.org/zh/)

### 安裝

```jsx
npm install vuex@next --save
```

### 引入

vue3 src/store目錄建立index.js

```jsx
import { createStore } from 'vuex' //引入

const store = createStore({
	state(){
		return{
			count:0,
		}
	}
})

export default store
```

main.js use 

```jsx
app.use(store)
```

### 模塊化

新建user.js

```jsx
const user = {
    state() {
        return {
            username: 'kazawan',
            age: 18
        }
    },
    getters: {
        getAge(state) {
            return state.age + ' years old111'
        }
    },
    mutations:{
        ageCheck(state){
            state.age = state.age + 1
        }
    }

}

export default user
```

index.js中引入

```jsx
import { createStore } from 'vuex'
import user from './user'

const store = createStore({
       modules:{
            users:user
       }
})

export default store;
```

### vue3 中使用

```jsx
<p>{{ $store.state.count }}</p>
```

computed中

```jsx
export default{
   computed:{
      gets(){
         return this.$store.state.count
      }
		}
}
```

### getters

```jsx
getters: {
        getAge(state) {
            return state.age + ' years old111'
        }
    },
```

vue3中使用

```jsx
computed:{
      gets(){
         return this.$store.getters.getAge
      }
}
```