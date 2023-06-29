# NPM 包制作

[手把手教你创建你的第一个 NPM 包](https://juejin.cn/post/6844903488153993229)

### 初始化npm init

![Untitled](NPM%20%E5%8C%85%E5%88%B6%E4%BD%9C%20f272335c0e6b4738b13d44d2e15c1968/Untitled.png)

### ~~根目录生成 /lib 生成文件 kazaloger.js~~

![Untitled](NPM%20%E5%8C%85%E5%88%B6%E4%BD%9C%20f272335c0e6b4738b13d44d2e15c1968/Untitled%201.png)

### ~~kazaloger~~.js

### 现在的项目结构

![Untitled](NPM%20%E5%8C%85%E5%88%B6%E4%BD%9C%20f272335c0e6b4738b13d44d2e15c1968/Untitled%202.png)

index.js

```jsx
function kazaloger(){
    console.log(`Welcome to KazaLoger`)
}

module.exports = kazaloger
```

.gitignore 排除不要上传的文件

```
node_modules/
a.js // 这是测试用的js文件
```

[npm 发布：包含或排除文件](https://cloud.tencent.com/developer/article/1890474)

### 使用npm默认源

```jsx
npm config set registry https://registry.npmjs.org
```

### npm login

```jsx
npm login
```

### 一系列登陆过程

输入账号密码邮箱

二次验证码打开手机googleauth（第三个码）

### 发布

```jsx
npm publish
```

发布成功

### 另外的项目引入

```jsx
npm i kaza-loger@latest --save
```

### index.js引入

```jsx
const loger = require('kaza-loger')
```