# Pinia 使用

[Pinia 🍍](https://pinia.vuejs.org/zh/)

# 安裝

```jsx
npm install pinia
```

vite 引入

```jsx
import { createPinia } from 'pinia'

app.use(createPinia())
```

scr/stores/[…foo.js]

計數器counter store //組合式

```jsx
import { defineStore } from 'pinia'
import { ref, computed } from 'vue'
//setup
export const useCounterStore = defineStore('counter', () => {
		//state
    const count = ref(0)
		//actions
    function add() {
        count.value++
    }
		//getters
    const getCount = computed(() => count.value +'$')
		////可傳參數的getters
    const addicon = computed((state) => {
        return (key)=>{
            return count.value + key
        }
    })

    return {
        count,
        add,
        getCount,
        addicon
    }
})
```

引用

官方推薦使用use[name]Store格式

```jsx
<script setup>
import {ref ,computed} from 'vue'
import { useCounterStore } from './stores/counter';

const counterStore = useCounterStore();

</script>
```

元素内應用

- state

```html
<p>{{ counterStore.count }}</p>
```

- actions

```html
<div @click="counterStore.add">...</div>
```

- getters

```html
<div >{{ counterStore.getCount }}</div>
```

- 帶參數的getters

```html
//countStore.count = 0 
<p>{{ counterStore.addicon('!!!') }}</p>
//返回count數值並添加 ！！！ output： 0!!!
```

## 多模塊

- /stores/[多個模塊]

```jsx
//計數器模塊
import { useCounterStore } from './stores/counter';//計數器模塊
import { useUserinfoStore } from './stores/userinfo';//用戶信息模塊

const counterStore = useCounterStore();
const userinfo = useUserinfoStore();
```

`stores/counter.js`

```jsx
import { ref, computed } from 'vue'
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }

  return { count, doubleCount, increment }
})
```

### 全局引入方法

```jsx
app.use(createPinia())
import { useCounterStore } from './stores/counter'
const counter = useCounterStore()
app.config.globalProperties.counter = counter
```

可以在任意地方使用直接使用counter

### 插件安装方法

`stores/index.js`

```jsx
import { useCounterStore } from "./counter";

export default{
    install:(app)=>{
        const counter = useCounterStore()
        app.config.globalProperties.counter = counter
    }
    
}
```

`main.js`

```jsx
import counter from './stores/index.js'
app.use(createPinia()) // 
app.use(counter)
```