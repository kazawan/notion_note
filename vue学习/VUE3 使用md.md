# VUE3 使用md

[在 vue3 中使用 markdown 编辑器 md-editor-v3 - 开源资源分享](http://www.yanzuoguang.com/article/1545.html#directory064477867401638128)

### 使用

```jsx
<template>
  <div id="md-editor-v3">z
    <MdEditor v-model="text" previewOnly/>
  </div> 
</template>

<script setup>
import  MdEditor  from 'md-editor-v3'
import md from './posts/test.md?raw'
import aaa from './posts/aaa.md?raw'
import 'md-editor-v3/lib/style.css'
import { ref } from 'vue';
const text = ref(aaa);
</script>
```

### vue3 读取md作为字符串的方法

```jsx
import md from './posts/test.md?raw'
import aaa from './posts/aaa.md?raw'
```