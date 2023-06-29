# ref 查找父元素

div元素 ref=”colitem”

```jsx
<template>
    <div class="kazalayoutconainersrow colitem" ref="colitem">
        <slot></slot>
    </div>
</template>
```

获取父元素

```jsx
colitem.value.offsetParent.clientWidth
```

获取父元素宽度 colitem.value.offsetParent.clientWidth

```jsx
colitem.value.offsetParent.clientWidth
            //父元素
```

```jsx
onMounted(() => {
    // const app = document.querySelector('#app')
    // console.log(colitem.value.offsetParent.clientWidth)
    window.addEventListener('resize', () => {
        windowWidth.value = colitem.value.offsetParent.clientWidth
        // console.log(windowWidth.value)
    })

})
```

获取自己的宽度

```jsx
colitem.value.clientWidth
```