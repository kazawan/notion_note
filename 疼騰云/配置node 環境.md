# 配置node 環境

### 安裝命令

setup_[版本號].x

```jsx
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

这里面 setup 是 13 那装的就是最新的，如果版本更新到 14 了 你改成 14 就行了

然后安装就可以了

```jsx
sudo apt-get install -y nodejs
```

最后验证一下，执行：nodejs -v 即可出现刚才安装的版本号。

这个时候 npm -v 也是最新的了

[npm does not support Node.js v10.19.0 · Issue #3644 · nodejs/help](https://github.com/nodejs/help/issues/3644)

![Untitled](%E9%85%8D%E7%BD%AEnode%20%E7%92%B0%E5%A2%83%206ef3cf900be44e6eab69b548165b41dc/Untitled.png)

```jsx
curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash -
sudo apt-get install -y nodejs
```

[Ubuntu 安装最新版本 Node.js](https://learnku.com/articles/42581)