# 初始化express

## 生成文件夹

```css
md dir
```

## npm 初始化

```css
npm init
```

一直下一步

## 修改package.json

![Untitled](%E5%88%9D%E5%A7%8B%E5%8C%96express%2056ec20e45d98484398f8e12586dfafea/Untitled.png)

```json
{
  "name": "ser4",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start":"node index.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "~4.16.1"
  }
}
```

## 下载依赖

```json
npm i
```

## 创建index.js

cmd命令 “file_name” 例:index.js

[小技巧-cmd常用命令之创建文件_sunpro518的博客-CSDN博客_如何新建cmd文件](https://blog.csdn.net/sunjinshengli/article/details/53557684)

```json
fsutil file createnew ["file_name"] 0
```

测试代码

```json
const express = require('express');
const app = express();
//!把vue生成好的dist文件夹拷贝到根目录 
app.use((express.static('dist')));
app.get('/', (req, res) => {
    res.sendFile('index.html')
})
app.listen(3000,()=>{
    console.log('listening on port 3000');
})
```

[Nodejs  express学习](../Nodejs%20express%E5%AD%A6%E4%B9%A0%204355ef5155fd460bb511b1780489c8ec.md)