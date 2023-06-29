# 简单搭建一个api

```jsx
const express = require('express');

const app = express();

app.all('*', function (req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS");
    res.header("X-Powered-By", ' 3.2.1')
    res.header("Content-Type", "application/json;charset=utf-8");
    next();
});

let data = {

    name: 'hello world'
}

app.get('/', (req, res) => {

    // res.setHeader('Content-Type', 'application/json');
    res.end(JSON.stringify(data))
})

app.listen(3000, () => { console.log('Server listening on port 3000') });
```