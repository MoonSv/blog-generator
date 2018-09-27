---
title: Node.js写脚本
date: 2018-09-18 20:36:55
tags:
---

## Node.js写脚本

JavaScript虽然和Java没什么关系，但是JS依然是一种脚本

1. 我们在Bash命令行里输入Bash命令，也可以再Node.js命令行里通过输入JS命令得到一样的结果(`Ctrl`+`D`退出)
2. Bash脚本能做的事情，JS脚本也能做（`sh demo.sh`对应`node demo.js`）

### 用JS切换目录

```javascript
console.log(process.cwd()) // 打印当前目录
// process.chdir('~/Desktop'); 这句话不行，因为JS不认识 ~ 目录
process.chdir("Users/Moonstone/Desktop")
console.log(process.cwd()) // 打印当前目录
```

### 用JS创建目录

```javascript
let fs = require("fs")
fs.mkdirSync("demo")
```

