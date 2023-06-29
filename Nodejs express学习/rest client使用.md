# rest client使用

[VSCode的REST Client指南，超好用的HTTP客户端工具 | 南瓜慢说官方网站 pkslow.com](https://www.pkslow.com/archives/vscode-rest-client)

新建一个test.http

各api之间需要用### 做分隔符

[api ] GET \ POST \ PUT \ DELETE

POST \PUT 需要写好header和要发送的json

```jsx
Content-Type: application/json
{
    "name":"hd3",
    "password":"11223365"
}

```

example:

```jsx
GET http://127.0.0.1:3000/

###

GET http://127.0.0.1:3000/api/user/6
###

GET http://127.0.0.1:3000/api/user/1

###

GET http://127.0.0.1:3000/api/user/0

###
POST http://127.0.0.1:3000/api/adduser HTTP/1.1
Content-Type: application/json

{
    "name":"hd3",
    "password":"11223365"
}

###
GET http://127.0.0.1:3000/api/users HTTP/1.1

###
PUT http://127.0.0.1:3000/api/change_password/1 HTTP/1.1
Content-Type: application/json

{
    "password":"111111"
}

###

DELETE  http://127.0.0.1:3000/api/del/5
```