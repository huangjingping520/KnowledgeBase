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

## http模块

http模块是Node.js提供的用来创建web服务器的模块。

**使用：**

```js
const http = require('http')
```

### req请求对象

`req`是请求对象，它包含了与客户端相关的数据和属性。

### res响应对象

`res.end()`向客户端发送指定的内容，并结束这次请求的处理过程。

**解决中文乱码问题：**调用`res.end()`方法时，向客户端发送中文内容时，会出现乱码内容，需要手动设置内容的编码格式。

```js
res.setHeader('Content-Type','text/html； charset = utf-8')
```

### 根据不同的URL响应不同的html内容

```js
server.on('request',(req,res) => {
  const url = req.url
  let content = '<h1>404 Not Found</h1>'

  if (url === '/' || url === '/index.html') {
    content = '<h1>首页</h1>'
  }else if (url === '/about.html') {
    content = '<h1>关于</h1>'
  }

  res.setHeader('Content-Type', 'text/html; charset=utf-8')

  res.end(content)
})
```

## 模块化

模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说模块化是可组合、分解后更换的单元。

编程领域中的模块化，就是遵守固定的规则，把一个打文件拆成独立并互相依赖的多个小模块。

**好处：**

- 提高了代码的复用性
- 提高了代码的可维护性
- 可以实现按需加载

### Node.js中模块的分类

- 内置模块
- 自定义模块
- 第三方模块

### 加载模块

使用`require()`方法

### 模块作用域

在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问显示，叫做模块作用域。

模块作用域能够防止全局变量污染的问题。

### 向外共享模块作用域中的成员

`module`对象

module对象中存储了和当前模块有关的信息。

`module.exports`对象

在自定义模块中，可以只用module.exports对象，将模块内容的成员共享出去，供外界使用。

`exports`对象

默认情况下，exports后module.exports指向同一个对象。

### CommmonJS规范

- 每个模块内部，module变量代表当前模块。
- module变量是一个对象，它的exports属性是对外的接口。
- 加载某个模块，其实是加载该模块的module.exports属性。

### 模块的加载机制

模块在第一次加载后会被缓存。模块会优先从缓存中加载，从而提高模块的加载效率。

内置模块的加载优先级最高。

## express

### 基本使用

导入express

```js
const express = require('express')

```

创建web服务器

```js
const app = express()
```

调用`app.listen()`，启动服务器

```js
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```

### 托管静态资源

`express.static()`

通过`express.static()`可以非常方便的创建一个静态资源服务器。

### express路由

广义上路由就是**映射关系**

在Express中路由是指 **客户端的请求** 与 **服务器处理函数**之间的映射关系

**组成：**
- 请求的类型
- 请求的URL地址
- 处理函数

```js
app.METHOD(PATH, HANDLER)
```

**路由的匹配过程**
每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果**请求类型**和**请求的URL**同时匹配成功，则Express会将这次请求转交给对应的function函数进行处理。

**模块化路由：**

为了方便对路由进行模块化管理，建议将路由抽离为单独的模块

1. 创建路由模块对应的.js文件
2. 调用express.Router()创建路由对象
3. 向路由对象上挂载具体的路由
4. 使用module.exports向外共享路由对象
5. 使用app.use()函数注册路由模块

### Express中间件

middleware，特指业务流程的中间处理环节。

本质就是一个function处理函数。

```js
function(req,res,next){
  next();
}
```

**next函数**是实现多个中间件连续调用的关键。表示把流转关系转交给下一个中间件或路由。

**中间件的作用：**
多个中间件之间，共享同一份req和res。基于这样的特性，可以再上游的中间件中，统一为req或res对象添加自定义的属性或方法，供下游的中间件或路由使用。

**错误级别中间件：**
用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

```js
app.use((err, req, res, next) => {
  console.log(err.message)
  res.send('Error!' + err.message)
})
```

**内置的中间件：**

`express.static`快速托管静态资源的内置中间件

`express.json`解析JSON格式的请求体数据

`express.urlencoded`解析URL-encoded格式的请求体数据

### CORS跨域资源共享

- 安装
- 导入
- 配置

```js
const cors = require('cors')
app.use(cors())
```

## Web开发模式
1. 服务端渲染的web开发模式
2. 前后端分离的新型web开发模式

### 服务端渲染的web开发模式

服务器发送给客户端的html页面是在服务器通过字符串拼接动态生成的。

**优点：**
1. 前端耗时少
2. 有利于SEO

**缺点：**
1. 占用服务端资源
2. 不利于前后端分离，开发效率低

### 前后端分离的Web开发模式

依赖于Ajax技术的广泛应用。即后端只负责提供API接口，前端使用Ajax调用接口的开发模式。

**优点：**
1. 开发体验好
2. 用户体验好
3. 减轻了服务器端的渲染压力

**缺点：**
1. 不利于SEO

## 身份认证

Authentication又称“身份验证”、“鉴权”，指通过一定的手段，完成对用户身份的确认。

- 服务端渲染推荐使用Session认证机制
- 前后端分离推荐使用JWT认证机制

### Session

> HTTP协议的无状态性

客户端端每次HTTP请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次HTTP请求的状态。

> Cookie

Cookie是存储在用户浏览器中的一段不超过4KB的字符串。由一个名称、一个值和其它几个用于控制Cookie有效期、安全性、使用范围的可选属性组成。

不同域名下的Cookie各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的Cookie一同发送到服务器。

**特性：**
1. 自动发送
2. 域名独立
3. 过期时限
4. 4KB限制

**Cookie的作用：**

客户端第一次请求服务器的时候，服务器会通过响应头的形式，向客户端发起一个身份认证的Cookie，客户端会自动讲Cookie保存在浏览器中。

随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份验证相关的Cookie，通过请求头的形式发送给服务器，服务器即可验证客户端的身份。

**Cookie不具有安全性**

> Session的工作原理

![](https://gitee.com/merlinalex/pic-go/raw/master/20220306220555.png)