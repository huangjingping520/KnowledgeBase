# <center>Node.js

Node.js是一个基于Chrome V8引擎的JavaScript运行环境

- 浏览器是JavaScript的前端运行环境
- Node.js是JavaScript的后端运行环境
- Node.js无法调用DOM和BOM等浏览器内置API

## fs文件系统模块

fs模块是Node.js官方提供的、用来操作文件的模块。其提供了一系列的方法和属性，用来满足用户对文件的操作需求。

**使用：**

```js
const fs = require('fs')
```

### 读取文件内容

`fs.readFile(path[,options], callback)`

1. 参数1：读取文件的存放路径
2. 参数2：读取文件时候采用的编码格式，一般默认指定 utf8
3. 参数3：回调函数，拿到读取失败和成功的结果  err  dataStr

### 向指定文件中写入内容

`fs.writeFile(file,data[,options], callback)`

1. 参数1：表示文件的存放路径
2. 参数2：表示要写入的内容
3. 参数3：回调函数

## path路径模块

path模块是Node.js提供的、用来处理路径的模块。其提供了一系列的方法和属性，用来满足用户对路径的处理需求。

**使用：**

```js
const path = require('path')
```

### 路径拼接

`path.join()`可以把多个路径片段拼接为完整的路径字符串

凡是涉及到路径拼接的操作，都要使用path.join()方法进行处理，而不是使用+进行字符串的拼接。

### 获取路径中的文件名

`path.basename()`可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名。

### 获取路径中的扩展名

`path.extname()`可以获取路径中的扩展名部分。