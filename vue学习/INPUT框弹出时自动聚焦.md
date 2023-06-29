# INPUT框弹出时自动聚焦

```jsx
onUpdated(() => {
    // console.log('updated')

    if (barShow.value) {

        nextTick(() => {
            i.value.focus()
        })
    } else {
        searchVal.value = ''
    }

})
```

这段代码是一个 Vue.js 的生命周期钩子函数 `onUpdated`，当组件更新时会被调用。在这个函数里，首先注释掉了一行打印更新信息的代码。接着，判断了 `barShow` 这个变量是否为真，如果是的话，就在下一个事件循环中调用 `i.value.focus()` 让 `i` 这个 DOM 元素获取焦点。如果 `barShow` 不为真，就将 `searchVal` 这个变量置为空字符串。这段代码的作用是在 `barShow` 变量值改变时，控制 `i` 元素是否获取焦点，并将 `searchVal` 变量置为空字符串。