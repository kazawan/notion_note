# css 记录

## 效果

参考网站

```jsx
https://a498390344.medium.com/localstorage%E5%AF%A6%E4%BD%9C%E4%B9%8Bto-do-list-8e8a996121c3
```

![Untitled](css%20%E8%AE%B0%E5%BD%95%202d253eb8386246e7aac82163dec30510/Untitled.png)

### app.vue

```jsx
<template>
  <p class="main">main 主要的元素</p>
  <p class="sub">sub 次要元素</p>
  <h1>LocalStorage實作之to do list</h1>
  <div class="line"></div>
  <div class="box">
    <div class="btn">
      <p>kazawan</p>
      <p>website</p>
      
    </div>
    <div class="btn2">
      <p>localStorage：可以跨瀏覽器分頁做使用、使用者關掉分頁或瀏覽器再打開資料仍不會消失，且資料無期效限制，資料將永久被保留。</p>
      <p>sessionStorage：生命週期較短，當使用者關掉瀏覽器或分頁時，sessionStorage 中的資料將被清空。當使用者關掉瀏覽器或分頁時，sessionStorage 中的資料將被清空</p>
      <p>資料儲存的格式 key 和 value 都只能接受「字串 」，若儲存的資料非字串 — 陣列或物件 — 在儲存時會被轉成字串格式，而衍伸問題</p>
      
    </div>
  </div>
  <img src="./img/topic.jpg" alt="" srcset="">

</template>

<style>
.box {
  width: 100%;
  display: flex;
}

.btn2{
  position: relative;
  width: 80%;
  height: 100px;
  background-color: var(--bg-color-sub);
  padding: 5px;
  border-radius: 10px;
  margin-top: 10px;
  margin-right: 2px;
  color: var(--text-color);
  overflow:hidden;
  text-overflow:ellipsis;
  padding-left: 20px;
}

.btn2::before{
  
  position: absolrute;
  top:10px;
  left:3px;
  width: 1%;
  content: "";
  height: 80%;
  width: 4px;
  border-radius: 10px;
  background-color: rgb(69, 133, 141);
}

.btn {

  width: 20%;
  height: 100px;
  background-color: var(--btn-color);
  padding: 5px;
  border-radius: 10px;
  margin-top: 10px;
  margin-right: 5px;
  color: var(--btn-text-color);
  overflow: hidden;
  transition: .3s ease-in ;
}

img{
  position: relative;
  top:10px;
  left: 0;
  width: 50%;
  height: 100%;
  border-radius: 10px;
  border: 1px solid var(--btn-color-hover) ;
  box-sizing: none;
}

.btn:hover {
  background-color: var(--btn-color-hover);

}

.line {
  width: 100%;
  height: 1px;
  background-color: var(--board-line);
  margin-top: 10px;
}

.main {
  color: var(--text-color);

}

.sub {
  color: var(--text-color-secondary)
}
</style>
```

### main.css

```jsx

@import './base.css';

:root{
  --bg-color:#e1dddd;
  --bg-color-sub:#d1cdcd;
  --text-color:#2e2d2dd0;
  --text-color-secondary:#666363;
  --btn-color:#2e2d2d;
  --btn-color-hover:#645656;
  --btn-text-color:#ffffff;
  --board-line:#2e2d2d5d;
  
}

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-family:sohne ;
  font-weight: normal;
  
  
}

h1{
  font-size: 32px;
  font-weight: 700;
  letter-spacing: -0.512px;
  line-height: 40px;
}

p span div {
  display: inline;
  
}

body{
  background-color: var(--bg-color);
}
```