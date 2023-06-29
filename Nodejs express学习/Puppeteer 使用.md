# Puppeteer 使用

[Puppeteer 简介 | Puppeteer 中文文档 | Puppeteer 中文网](https://puppeteer.bootcss.com/)

example

```jsx
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('https://example.com');
  await page.screenshot({path: 'example.png'});

  await browser.close();
})();
```

### 拦截请求示例

```jsx
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch()
  const page = await browser.newPage()

  await page.setViewport({ width: 1200, height: 800 })

  await page.setRequestInterception(true)

  page.on('request', (request) => {
    console.log('>>', request.method(), request.url())
    request.continue()
  })

  page.on('response', (response) => {
    console.log('<<', response.status(), response.url())
  })

  await page.goto('https://danube-webshop.herokuapp.com/')

  await page.screenshot({ path: 'screenshot.png' })

  await browser.close()
})()
```

运行后得到

```jsx
>> GET https://danube-webshop.herokuapp.com/
<< 200 https://danube-webshop.herokuapp.com/
>> GET https://kit.fontawesome.com/1a858c55db.js
>> GET https://danube-webshop.herokuapp.com/static/css/app.170c518fd30e61cd11c4b17e7c98fd47.css
>> GET https://danube-webshop.herokuapp.com/static/js/manifest.2ae2e69a05c33dfc65f8.js
>> GET https://danube-webshop.herokuapp.com/static/js/vendor.dcf85801186ed8506b50.js
>> GET https://danube-webshop.herokuapp.com/static/js/app.5bd54d5a0aa84966f389.js
<< 200 https://danube-webshop.herokuapp.com/static/js/vendor.dcf85801186ed8506b50.js
<< 200 https://danube-webshop.herokuapp.com/static/js/manifest.2ae2e69a05c33dfc65f8.js
<< 200 https://danube-webshop.herokuapp.com/static/css/app.170c518fd30e61cd11c4b17e7c98fd47.css
<< 200 https://kit.fontawesome.com/1a858c55db.js
>> GET https://ka-f.fontawesome.com/releases/v5.15.4/css/free.min.css?token=1a858c55db
>> GET https://ka-f.fontawesome.com/releases/v5.15.4/css/free-v4-shims.min.css?token=1a858c55db
>> GET https://ka-f.fontawesome.com/releases/v5.15.4/css/free-v4-font-face.min.css?token=1a858c55db
<< 200 https://danube-webshop.herokuapp.com/static/js/app.5bd54d5a0aa84966f389.js
>> GET https://danube-webshop.herokuapp.com/static/logo-horizontal.svg
>> GET https://danube-webshop.herokuapp.com/api/books
<< 200 https://ka-f.fontawesome.com/releases/v5.15.4/css/free.min.css?token=1a858c55db
<< 200 https://ka-f.fontawesome.com/releases/v5.15.4/css/free-v4-font-face.min.css?token=1a858c55db
<< 200 https://danube-webshop.herokuapp.com/api/books
<< 200 https://ka-f.fontawesome.com/releases/v5.15.4/css/free-v4-shims.min.css?token=1a858c55db
>> GET https://ka-f.fontawesome.com/releases/v5.15.4/webfonts/free-fa-solid-900.woff2
>> GET https://ka-f.fontawesome.com/releases/v5.15.4/webfonts/free-fa-solid-900.woff2
<< 200 https://danube-webshop.herokuapp.com/static/logo-horizontal.svg
<< 200 https://ka-f.fontawesome.com/releases/v5.15.4/webfonts/free-fa-solid-900.woff2
```

### 打开拦截

```jsx
await page.setRequestInterception(true)
```

### 监控请求

```jsx
page.on('request',(request)=>{
		//dosomthing ....
		request.continue()
})
```

### 监控响应

```jsx
page.on('response', (response) => {
      //dosomthing...
})
```