# vue3 自定义指令模态框

## 建立`hooks/el/getel.js`

```jsx
const getel = (el,binding) =>{
		console.log(el,binding.value)
    el.style.transition = '1s all ease'
    el.style.backgroundColor = binding.value
    
}

export default getel
```

## 建立`hooks/el/index.js`

```jsx
import getel from './getel.js'//引入需要的函数

export default {
    install: (app) => {
        app.directive('showel', {
            // 指令的生命周期函数
            mounted:(el,binding)=>{
                // 获取元素
                getel(el,binding)
            },
            updated:(el,binding)=>{
                // 获取元素
                getel(el,binding)
            }
        })
    }
}
```

## `main.js` 全局引入

```jsx
import getel from './hooks/el/index.js'
app.use(getel)
```

## `App.vue` 使用

```jsx
<template>
<!-- 这是一个简单的div -->
<div v-showel="hd"  >box</div>
<!-- 这是一个简单的按钮 -->
<button @click="changcolor">chang</button>
</template>

<script setup>
import { ref } from 'vue';

// 定义一个响应式变量
const hd =ref('#ccc')

// 定义一个改变颜色的方法
const changcolor = () =>{
  hd.value  =  '#007acc'
}
</script>
```

在 Vue3 自定义指令中，`binding` 是一个对象，包含指令的相关信息，如指令的值、参数、修饰符等。可以通过 `binding.value` 获取指令的值，通过 `binding.arg` 获取指令的参数，通过 `binding.modifiers` 获取指令的修饰符。需要注意的是，在使用修饰符时，需要在指令名后面添加一个 `.`，例如 `v-my-directive.prevent`。

此文档中提供了两个自定义指令：`showel` 和 `toolbar`。

### `showel` 自定义指令使用方法

此自定义指令可以用于改变元素的背景颜色。在 `hooks/el/getel.js` 中定义了相关的函数，具体的实现细节可以查看源代码。在 `hooks/el/index.js` 中，将 `showel` 指令与 `getel` 函数绑定，这样当指令被使用时，相关的函数就会被调用。在 `App.vue` 中，我们使用了一个 `div` 元素和一个按钮，用于测试自定义指令的效果。当点击按钮时，`div` 元素的背景颜色会发生改变。

使用步骤：

1. 将 `hooks/el/getel.js` 和 `hooks/el/index.js` 复制到你的项目中。
2. 在 `main.js` 中全局引入 `hooks/el/index.js`。
3. 在需要使用的元素上添加 `v-showel` 指令，并指定颜色值。

示例代码如下：

```
<template>
<!-- 这是一个简单的div -->
<div v-showel="hd"  >box</div>
<!-- 这是一个简单的按钮 -->
<button @click="changcolor">chang</button>
</template>

<script setup>
import { ref } from 'vue';

// 定义一个响应式变量
const hd =ref('#ccc')

// 定义一个改变颜色的方法
const changcolor = () =>{
  hd.value  =  '#007acc'
}
</script>

```

### `toolbar` 自定义指令使用方法

此自定义指令可以用于在元素上添加提示信息。在 `hooks/kazagetel.js` 中定义了相关的函数，具体的实现细节可以查看源代码。在 `main.js` 中，将 `toolbar` 指令与 `kazagetel` 函数绑定，这样当指令被使用时，相关的函数就会被调用。在 `App.vue` 中，我们使用了一个 `div` 元素，用于测试自定义指令的效果。当鼠标点击 `div` 元素时，会弹出提示框。

使用步骤：

1. 将 `hooks/kazagetel.js` 复制到你的项目中。
2. 在 `main.js` 中全局引入 `hooks/kazagetel.js`。
3. 在需要添加提示信息的元素上添加 `v-toolbar` 指令，并指定提示信息。

示例代码如下：

```
<template>
  <div class="dash" tips="version v1.0.1" data="aaa" v-toolbar >DashBoard</div>
</template>

```

```jsx
<div class="dash" tips="version v1.0.1" data="aaa" v-toolbar >DashBoard</div>
```