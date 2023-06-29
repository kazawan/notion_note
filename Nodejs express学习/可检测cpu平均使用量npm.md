# 可检测cpu平均使用量npm

[npm: node-os-utils](https://www.npmjs.com/package/node-os-utils)

在 Node.js 中，我们可以使用 [node-os-utils](https://www.npmjs.com/package/node-os-utils) 库来检测 CPU 的平均使用量。

以下是一个简单的示例代码，可以获取 CPU 的平均使用量：

```
var osu = require('node-os-utils')
var cpu = osu.cpu

var count = cpu.count() // 8

cpu.usage()
  .then(cpuPercentage => {
    console.log(cpuPercentage) // 10.38
  })

```