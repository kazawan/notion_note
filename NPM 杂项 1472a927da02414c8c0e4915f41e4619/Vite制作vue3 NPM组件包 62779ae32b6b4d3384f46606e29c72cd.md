# Vite制作vue3 NPM组件包

## 新建项目

```jsx
npm init vite@latest
```

- 选择vue
- 生成packages文件夹 → 组件库的名字 →[ 组件文件夹 +  index.js]

![Untitled](Vite%E5%88%B6%E4%BD%9Cvue3%20NPM%E7%BB%84%E4%BB%B6%E5%8C%85%2062779ae32b6b4d3384f46606e29c72cd/Untitled.png)

- index.js

```jsx
import kazaCharts from './chart/kazaCharts.vue'
import kazaProgressBar from './ProgressBar/kazaProgressBar.vue'

export default {
    install:(app)=>{
        app.component('kazaCharts', kazaCharts)
        app.component('kazaProgressBar', kazaProgressBar)
    }
}
```

- vue组件命名

```jsx
<script>
export default {
    name:'kazaCharts'
}
</script>
```

- vite.config.js修改

```jsx
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import  { resolve } from 'path';

export default defineConfig({
	plugins: [vue()],
	build: {
		outDir: 'lib',
		lib: {
			entry: resolve(__dirname, 'packages/kazaUI/index.js'), //指定组件编译入口文件
			name: 'kazaui',
			fileName: 'kazaui',
		},//库编译模式配置
		rollupOptions: {
			// 确保外部化处理那些你不想打包进库的依赖
			external: ['vue'],
			output: {
				// 在 UMD 构建模式下为这些外部化的依赖提供一个全局变量
				globals: {
					vue: 'Vue',
				},
			},
		},// rollup打包配置
	},
});
```

- 打包 #先修改package.json中script的build命令为"build": "vite build",

```jsx
npm run build 

```

- package.json修改

```jsx
{
  "name": "kaza-ui",//项目名字
  "private": false,//需修改为false 否则要付费😄
  "version": "0.0.7",//版本号
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "less": "^4.1.3",
    "vue": "^3.2.45"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^4.0.0",
    "vite": "^4.1.0"
  },
  "main": "lib/kazaui.umd.cjs" // 打包后生成的umd环境下的js文件 此条非常重要
}
```

## 🎯发布

参考此处

[NPM 包制作](NPM%20%E5%8C%85%E5%88%B6%E4%BD%9C%20f272335c0e6b4738b13d44d2e15c1968.md)