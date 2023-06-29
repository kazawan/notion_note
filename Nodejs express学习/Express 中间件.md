# Express 中间件

[Express中间件_夏至か未至的博客-CSDN博客_express 中间件](https://blog.csdn.net/weixin_45650502/article/details/123752147)

## 根目录创建src文件夹

创建loger.js

./src/loger.js

```jsx
const midlog = function(req, res, next) {
    console.log('this is from log.js')
		
		//注意需要加上next（）
		next();
}

module.exports = midlog
```

所有路由都会先过一遍中间间

![Untitled](Express%20%E4%B8%AD%E9%97%B4%E4%BB%B6%20e4281b96b3484922aeb2eb366b5ecf19/Untitled.png)

### 全局引用

```jsx
const express = require('express')
const router = express.Router()
//引入中间件
const loger = require('../src/log.js')
//这里代表局引用
router.use(loger)

router.get('/', (req, res) => {
    res.end(`hello world from router`)
})

router.get('/test', (req, res) => {
    res.end(`test from router`)

})

module.exports = router
```

关于express 路由router的看这里

[Express Router使用](Express%20Router%E4%BD%BF%E7%94%A8%20e1deb32a792c499c89b1e2e047b2af5f.md) 

### 局部引用

```jsx
const express = require('express')
const router = express.Router()
const loger = require('../src/log.js')

// router.use(loger)

//在路由上添加loger局部引用
router.get('/',loger,(req, res) => {
    res.send(`hello world from router`)
})
// /test路由没有引用loger
router.get('/test', (req, res) => {
    console.log(req.originalUrl)
    console.log('no midwear')
    res.send(`test from router`)

})

module.exports = router
```

部分引用得结果

![Untitled](Express%20%E4%B8%AD%E9%97%B4%E4%BB%B6%20e4281b96b3484922aeb2eb366b5ecf19/Untitled%201.png)

### 多个局部引用

```jsx
const { application } = require('express')
const express = require('express')
const router = express.Router()
//引入两个中间件
const loger = require('../src/log.js')
const loger2 = require('../src/log2.js')

// router.use(loger)
// router.use(loger2)

//loger ，loger2 两个引用到一个路由中
router.get('/',loger,loger2,(req, res) => {
    res.send(`hello world from router`)
})

router.get('/test', (req, res) => {
    console.log(req.originalUrl)
    console.log('no midwear')
    res.send(`test from router`)

})

module.exports = router
```