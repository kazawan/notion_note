# Vue引入Bootstrap方法

## npm 安装bootstrap

```powershell
npm i bootstrap
```

## 安装 Popper.js

Popper.js 是 Bootstrap 4 的依赖项，用于显示弹出窗口。它是引导程序的对等依赖项，这意味着它是引导程序需要但在安装时不包含在自身中的东西。所以要安装 popper.js 运行.

bootstrap5 需要这个

```powershell
npm install @popperjs/core --save
```

## 在main.js引入

```jsx
import "bootstrap";
import "bootstrap/dist/css/bootstrap.css"
```

## App.vue测试

```html
<button type="button" class="btn btn-primary">Primary</button>
```

### Bootstrap V5 中文文档

[Get started with Bootstrap](https://v5.bootcss.com/docs/getting-started/introduction/)