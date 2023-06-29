# vue Element Plus引入

### 安装

```jsx
npm install element-plus --save
```

### main.js 注册

```jsx
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'

const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

### 测试

```jsx
<el-button type="primary">Primary</el-button>
```

### icon引入

```jsx
npm install @element-plus/icons-vue
```

### main.js全局

```jsx
import * as ElementPlusIconsVue from '@element-plus/icons-vue'

const app = createApp(App)
for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
  app.component(key, component)
}
```

### .vue文件script 引入

```jsx
import { Close, Select } from '@element-plus/icons-vue';
```

# 按需自动引入

[vue3+vite使用element plus自动按需导入_前端菜鸟丶Ndie的博客-CSDN博客_elementplus自动导入](http://t.csdn.cn/QExgx)

安装unplugin-vue-components  

和 unplugin-auto-import

```jsx
npm install -D unplugin-vue-components unplugin-auto-import
```

vite.config.js引入

```jsx
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'
```

plugins这项改为

```jsx
plugins: [vue(),//这是原来有的
			//这是后加的
      AutoImport({
        resolvers: [ElementPlusResolver()],

      }),
      Components({
        resolvers: [ElementPlusResolver()],
      })        
  ],
```

 

### 图标导入

```jsx
import 'element-plus/dist/index.css';// element plus样式
import * as ElIcons from '@element-plus/icons-vue' //element plus图标

const app = createApp(App)

//这是需要的语句
for (const name in ElIcons) {
  app.component(name, (ElIcons)[name]);
}

app.mount('#app')

```

app.vue测试

```jsx
<el-icon><Search /></el-icon>
```