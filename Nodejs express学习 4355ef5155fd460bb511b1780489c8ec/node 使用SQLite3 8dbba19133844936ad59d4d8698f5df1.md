# node 使用SQLite3

[nodejs使用Express+sqlite3实现RESTful API http服务器的增删改查_邱六崇的博客-CSDN博客_express sqlite](https://blog.csdn.net/qq_39425927/article/details/107541997)

### 客户端使用

[SQLite3 HeidiSQL.exe使用](SQLite3%20HeidiSQL%20exe%E4%BD%BF%E7%94%A8%2071f6af92c2b54fde957d361fc8ad432e.md) 

### index.js 引入

```jsx
var sqlite3 = require('sqlite3').verbose();
const express = require('express');
const bodyParser = require('body-parser');
```

### app.use

```jsx
// 使用body-parser,支持编码为json的请求体
app.use(bodyParser.json());
// 支持编码为表单的消息体
app.use(bodyParser.urlencoded(
    {
        extended: true
    }
))
```

### 跨域问题

[CORS跨域问题](CORS%E8%B7%A8%E5%9F%9F%E9%97%AE%E9%A2%98%20b94267d9cc4f40aea15c52a63a6d0471.md) 

```jsx
app.all('*', function (req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS");
    res.header("X-Powered-By", ' 3.2.1')
    res.header("Content-Type", "application/json;charset=utf-8");
    next();
});
```

### 创建数据库

```jsx
//语法
// new sqlite3.Database([db_name],cb)

const sqlite3 = require('sqlite3').verbose();
const db = new sqlite3.Database([db_name],(err)=>{
			if (err){
          console.log(err);
      } else {
          console.log(`${dbName}.sqlite3 created`);
      }
})

```

### 创建表

```jsx

//语法
//creat table if not exists [*TABLE NAME*]([OPTION]),CALLBACK
db.run(`create table if not exists [*TABLE NAME*](id INTEGER PRIMARY KEY AUTOINCREMENT,
																									name TEXT,
																									password TEXT ,
																									adminLevel int )`,(err)=>{
						if (err) {
                console.log(err);
            } else {
                console.log(`table:${tableName} created`);
            }
})
```

### 查询

查询全部

```jsx
//语法：
//'select * from [表] ，(err,data)=>{console.log(data)}
//user为数据库的表  rows为返回的数据
app.get('/api/users', (req, res) => {
    db.all('select * from user', (err, rows) => {
        res.end(JSON.stringify(rows))
    })
    
})
```

查询单个项目

```jsx
//api需加一个next
app.get('[api]',(req,res,next)=>{})
//语法：
//'select * from [表] where [项目] = ?',[项目传参]，(err,data)=>{console.log(data)}

//查询_id 
db.get('select * from user where _id = ?', [req.params.id], (err, data) => {
                if (err) {
                    console.log('fail')
                    return next(err)
                }
                res.send(data)
    })
```

### 插入一个数据

```jsx
app.post('[api]', (req, res) => {
//例如需要name，password两个项目
//语法：
//'insert into [表]([项目传参]) values(?,?//有多少个就有多少个问好)'，[项目传参]，（err）
    db.run('insert into user(name,password) values(?,?)', [req.body.name, req.body.password], (err) => {
        if (err) throw err;
        console.log('insert success');
    })
})
```

### 修改一个数据

```jsx
//[api]中的：id 需要提供一个id，url：http://127.0.0.1:3000/api/change_password/1
//Content-Type: application/json
//提供要修改的数据
//{
//    "password":"000000000"
//}

//语法：
//'updata [表] set [项目]=? where [id] =? ',[项目传参，id传参]
app.put('/api/change_password/:id',(req,res)=>{
    db.run('update user set password =? where _id =?', [req.body.password,req.params.id],(err)=>{
        if(err) throw err;
        console.log('update success');
    })
})
```

### 删除一个数据

```jsx
//[api]中的：id 需要提供一个id url：http://127.0.0.1:3000/api/del/5
//语法：
// 'delete from [表] where [项目]=?',[项目传参],(err)=>{if(err) throw err}
app.delete('/api/del/:id',(req,res)=>{
    db.run('delete from user where _id =?', [req.params.id], (err) => {
        if(err) throw err;
        console.log('delete success');
    })    
})
```

[Bodyparse 返回空白值问题](Bodyparse%20%E8%BF%94%E5%9B%9E%E7%A9%BA%E7%99%BD%E5%80%BC%E9%97%AE%E9%A2%98%20e398729f56d641a98d1606adf946410b.md) 

这个解决返回值问题

### example

```jsx
var sqlite3 = require('sqlite3').verbose();
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

// 使用body-parser,支持编码为json的请求体
app.use(bodyParser.json());
// 支持编码为表单的消息体
app.use(bodyParser.urlencoded(
    {
        extended: true
    }
))

var db = new sqlite3.Database('./db/data.sqlite3');

let hd = {
    name: 'hd2',
    password: 'password',

}

// db.run('insert into user(name,password) values(?,?)',[hd.name,hd.password], (err)=>{
//     if(err) throw err;
//     console.log('insert success');

// })

//test
app.get('/', (req, res) => {
    res.end('hello world');

})

app.get('/api/users', (req, res) => {
    db.all('select * from user', (err, rows) => {
        res.end(JSON.stringify(rows))
    })
    // res.setHeader('Content-Type', 'application/json');
})

app.get('/api/user/:id', (req, res, next) => {
    db.all('select * from user', (err, rows) => {
        if (req.params.id > rows.length || req.params.id == 0) {
            res.end('user not found')
        } else {
            db.get('select * from user where _id = ?', [req.params.id], (err, rows) => {
                if (err) {
                    console.log('fail')
                    return next(err)
                }
                res.send(rows)
            })
        }

    })

})

app.post('/api/adduser', (req, res) => {
    db.run('insert into user(name,password) values(?,?)', [req.body.name, req.body.password], (err) => {
        if (err) throw err;
        console.log('insert success');
    })
})

app.put('/api/change_password/:id', (req, res) => {
    db.run('update user set password =? where _id =?', [req.body.password, req.params.id], (err) => {
        if (err) throw err;
        console.log('update success');
    })
})

app.delete('/api/del/:id', (req, res) => {
    db.run('delete from user where _id =?', [req.params.id], (err) => {
        if (err) throw err;
        console.log('delete success');
    })
})

app.listen(3000, () => { console.log('Server listening on port 3000') });
```

### 异步返回

在判断的时候需要异步返回

```jsx
async findOne(tableName,name){
        let result = new Promise((resolve)=>{
            this.db.all(`select * from ${tableName} where name =?`,[name],(err,data)=>{
                if(err){
                    console.log(err);
                }else{
                    resolve(data);
                }
            })
        })
        return result
    }
```

```jsx
//接受
aa.findOne('adminlist',req.body.name).then((data)=> {
        console.log(data.length)
        if(data.length === 0 ){
            next()
        }else{
                console.log('名字重复了')
            return
        }
        
   })
```