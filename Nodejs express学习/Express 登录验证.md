# Express 登录验证

[Express中jwt验证的简单使用](https://juejin.cn/post/7124510066509611016#heading-8)

需要在客户端axios传入带token的headers

[Vue3使用axios](https://www.notion.so/Vue3-axios-41db1033b5f44e5594985df4c95fbc24?pvs=21) 

```jsx
const jwt = require("jsonwebtoken");
const { expressjwt } = require("express-jwt");
const express = require("express");
const bodyParser = require("body-parser");
const cors = require("cors");

const app = express();
const key = "kazawan"

app.use(cors());
app.use(expressjwt({ secret: key, algorithms: ["HS256"] }).unless({ path: ['/api/login'] }));

app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use((err, req, res, next) => {
    console.log(req.headers.authorization)
    if (err.name === "UnauthorizedError") {
        return res.send({
            code: 401,
            msg: "无效的token",
        });
    }
    res.send({
        code: 500,
        msg: "未知的错误",
    });
    next()
})

app.get('/hello',(req, res) => {
    res.send({
        code: 1,
        msg: "hello world"

    })
})

app.post("/api/login", (req, res) => {
    const userinfo = req.body
    console.log(userinfo)

    if (userinfo.username != "kazawan") {
        return res.send({
            "code": 0,
            "msg": "用户名错误"

        })
    } else {
        const token = jwt.sign(
            {
                username: userinfo.username,
                level: "白金用户",

            },
            key, { expiresIn: '30s' })
        res.send({
            "code": 1,
            "msg": "登陆成功",
            "token": "Bearer" + " " + token, // 要发送给客户端的 token 字符串

            //Bearer 
        })
    }

})

app.post('/api/userinfo', (req, res) => {
    console.log(req.body)
    const a = req.headers.authorization
    const auth = req.headers.authorization.split(' ')[1]
    console.log(auth)
    if(req.header === undefined){

    }
    jwt.verify(auth, key, (err, decoded) => {
        if (err) {
            console.log(`jwt:${err.message}`)
            return res.send({
                "msg": "fail"
            })
        } else {
            req.user = decoded;
            console.log(req.user);
            res.send({
                code: 1,
                msg: "获取用户",
                data: req.user

            })
        }

    })

})

app.listen(3000, () => {
    console.log('http://0.0.0.0:3000')

})
```

[Express + Session 实现登录验证_commissionor的博客-CSDN博客](https://blog.csdn.net/qq_43051529/article/details/82871417?ops_request_misc=&request_id=&biz_id=102&utm_term=express%20+%20session%20%E5%AE%9E%E7%8E%B0%E7%99%BB%E9%99%86%E9%AA%8C%E8%AF%81&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-82871417.142^v73^control,201^v4^add_ask,239^v1^insert_chatgpt&spm=1018.2226.3001.4187)

```jsx
const express = require('express')
const dotenv = require('dotenv')
const bodyparser = require('body-parser')
const session = require('express-session');
const cors = require('cors')

const app = express();

app.use(bodyparser.json()); // 使用bodyparder中间件，
app.use(bodyparser.urlencoded({ extended: true }));
app.use(cors())
dotenv.config();

app.use(session({
    secret: process.env.SECRET_KEY,
    resave: true,
    saveUninitialized: true,
    cookie: {
        maxAge: 1000 * 60

    }
}))

app.get('/', (req, res) => {
    if (req.session.userName === "kazawan") {
        res.redirect('/getSession')
    } else {
        res.send(`<h1>NOT LOGIN</h1>
    <a/ href="http://localhost:3000/getSession">LOGIN </a>
`)
    }

})

app.get('/getSession', (req, res) => {
    req.session.userName = "kazawan";
    req.session.userPass = "00189423";
    res.send(`<h1>Session Get</h1>
                <a/ href="http://localhost:3000/login">Login</a>
    `);

});

app.get('/login', (req, res) => {
    if (req.session.userName === "kazawan") {
        res.send(`
            <h1>welcome kazawan</h1>
            <a/ href="http://localhost:3000/logout">LOGOUT </a>
        `);
    } else {
        res.redirect('/')
    }
})

app.get('/logout', (req, res) => {
    req.session.userName = null
    req.session.userPass = null
    res.redirect('/')
})

ports = process.env.PORT || 8080

app.listen(ports, () => { console.log(`listening on:http://localhost:${ports}`) });
```

- [x]  未验证