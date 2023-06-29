# vue初始化

[Quick Start | Vue.js](https://vuejs.org/guide/quick-start.html#creating-a-vue-application)

```jsx
npm init vue@latest
```

```jsx
cd dir
npm i
npm run dev //测试
```

# 修改css

```powershell
	./src/assets/main.css
```

修改#app

```css
#app {
    display: grid;
    grid-template-columns: 1fr;
    padding: 0 2rem;
  }
```

## 修改vite.config.js

```jsx
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  //添加这行 否侧生成的dist文件显示为空白
  base:'./',
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})
```

[vue学习](../vue%E5%AD%A6%E4%B9%A0%20425d59a0ed0f49b28bc7120c73fa3909.md)