# Express Router使用

### 新建routes文件夹

![Untitled](Express%20Router%E4%BD%BF%E7%94%A8%20e1deb32a792c499c89b1e2e047b2af5f/Untitled.png)

新建router.js

```jsx
const express = require('express')
const router = express.Router()

router.get('/',loger,loger2,(req, res) => {
    res.send(`hello world from router`)
})

router.get('/test', (req, res) => {
    console.log(req.originalUrl)
    console.log('no midwear')
    res.send(`test from router`)

})

//导出一下
module.exports = router
```

在index.js中使用

```jsx
const express = require('express')
const app = express()
//引入router
const router = require('./routes/router')

//全局引用
app.use(router)

app.listen(3000, function () {
    console.log('http://localhost:3000')
})
```