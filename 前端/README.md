## HTML
## Flex布局
- 浏览器**提倡**的布局模型
- 布局网页更简单、灵活
- 避免浮动脱标的问题

```css
display: flex;

justify-content: ; /* 调整主轴对齐方式*/
/* 
center: 居中
space-between: 间距在盒子之间
space-evenly: 所有地方间距相等
space-around: 盒子两侧增加间距
*/

align-items: ; /* 调节测轴对齐方式*/
/* 
center: 垂直居中;
stretch: 拉伸（默认值）;
*/
```

- 使用`flex-direction`改变元素排列方向

> row: 行，水平（默认值）
> column: 列，垂直
> row-reverse: 行，从右向左
> column-reverse: 列，从下向上

- 使用`flex-wrap`实现弹性盒子**多行**排列效果

## 移动适配
网页元素宽高尺寸随设备尺寸变化

- `rem`: 目前多数企业在用的解决方案
- `vw/vh`: 未来的解决方案

### `rem`
- 相对单位
- rem单位是相对于HTML标签的自豪计算结果
- 1rem = 1HTML字号大小

### 媒体查询
媒体查询能够检测视口的宽度，然后编写差异化的CSS样式

```css
@media (媒体特性) {
  选择器 {
    CSS属性
  }
}
```

目前rem布局方案中，将网页等分成10份，HTML标签的字号位视口宽度的1/10

### flexible.js

### `vw.vh`

相对单位，相对视口的尺寸计算结果

- vw: viewport width
  - 1vw = 1 / 100 视口宽度
- vh: viewport height
  - 1vh = 1 / 100 视口高度

## less
Less是一个CSS预处理器，Less文件后缀是`.less`

扩充了CSS语言，使CSS具备一定的逻辑性、计算能力

**注意：浏览器不识别Less代码，目前，网页要引入对应的CSS文件**

Less进行数学运算时，加、减、乘都可以直接书写计算表达式，但除法需要添加`()`或者`.`

```less
.box {
  width: 100 + 50px;
  height: 5 * 32px;

  width: (100 / 4px);
  height: 100 ./ 4px;
}

```

### Less变量

> 定义变量：`@变量名: 值;`
> 
> 使用变量：`CSS属性: @变量名;`

### Less导入

**语法：**

当导入文件位less时，可以省略后缀`.less`

```less
@import '文件路径';
```

### Less导出

在less文件开头

```less
// out: 导出路径
```

### 禁止导出

```less
// out: false
```

## 响应式

### 媒体查询

能够根据设备宽度的变化，设置差异化样式

```css
@media (媒体特性) {
  选择器 {
    样式
  }
}
```

媒体特性常用写法：

- max-width

从大到小书写

- min-width

从小到大书写

## BootStrap

使用栅格系统布局响应式网页

|          | 超小屏幕   | 小屏幕     | 中等屏幕   | 大屏幕     |
| :------- | :--------- | :--------- | :--------- | :--------- |
| 响应断点 | <768px     | >=768px    | >=992px    | >=1200px   |
| 别名     | `xs`       | `sm`       | `md`       | `lg`       |
| 容器宽度 | 100%       | 750px      | 970px      | 1170px     |
| 类前缀   | `col-xs-*` | `col-sm-*` | `col-md-*` | `col-lg-*` |
| 列数     | 12         | 12         | 12         | 12         |
| 列间隙   | 30px       | 30px       | 30px       | 30px       |

`.container` 默认指定宽度且居中

`.container-fluid` 宽度均为100%

## AJAX

> URL地址

全称`UniformResourceLocator` 中文为 **统一资源定位符**，用于标识互联网上每个资源的唯一存放位置。

浏览器只有通过URL地址，才能正确定位资源的存放位置，从而成功访问到对应的资源。

**组成部分：**
- 客户端与服务器之间的通信协议
- 存有该资源的服务器名称
- 资源在服务器上具体的存放位置

> 网页的打开过程

1. 客户端请求服务器
2. 服务器处理这次请求
3. 服务器响应客户端

**请求-处理-响应**

> 资源的请求方式

**GET**

通常用于获取服务端资源

**POST**

通常用于向服务器提交数据

> AJAX的概念

全称为Asynchronous JavaScript And XML（异步JavaScript和XML）

通俗的理解就是在网页中利用**XMLHttpRequest**对象和服务器进行数据交互的方式

> 接口

**概念：**
使用Ajax请求数据时，被请求的URL地址，就叫数据接口（简称接口）。每个接口必须有请求方式。

> `<form>`标签的属性

`enctype`属性：

| 值 | 描述 |
| :--- | :--- |
| application/x-www-form-urlencoded | 在发送前编码所有字符（默认） |
| multipart/form-data | 不对字符编码。**在使用包含文件上传控件的表单时必须使用该值。** |
| text/plain | 空格转换为“+”，但不对特殊字符编码。（很少用） |

> 表单同步提交的缺点

1. 表单同步提交后，整个页面会发生跳转，跳转到action URL所指向的地址。
2. 页面之前的状态后数据都会丢失。

> 解决方法

表单只负责采集数据，Ajax负责将数据提交到服务器。

> 模版引擎

1. 减少了字符串拼接操作
2. 使代码结构更清晰
3. 使代码更易于阅读与维护

## XMLHttpRequest

> URL编码

URL地址中，只允许出现英文相关的字母、标点符号后数字，所以不允许出现中文字符。

所以如果URL中需要包含中文这样到字符，则必须对中文字符进行**转码**。

URL编码的原则： 使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。

> 如何对URL进行编码和解码

- encodeURI() 编码函数
- decodeURI() 解码函数

> 数据交换格式

服务端与客户端之间进行数据传输与交换的格式

前端经常提及的两种数据交换格式为`XML`和`JSON`，其中`JSON`使用较多

> XML

`XML`即EXtensible Markup Language，可扩展标记语言

XML与HTML虽然都是标记语言，但是两者之间没有任何的关系

- HTML被设计用来描述网页上的内容，是网页内容的载体
- XML被设计用来传输和存储数据，是数据的载体

XML的缺点：
1. 格式臃肿，和数据无关的代码多，体积大，传输效率低
2. 在JavaScript中解析XML比较麻烦

> JSON

JSON即JavaScript Object Notation,JavaScript对象表示法。

JSON就是JavaScript对象和数组的字符串表示法。

JSON的本质是字符串。

把数据对象转换为字符串的过程，叫做序列化。 如：`JSON.stringify()`函数

把字符串转换为数据对象的过程，叫做反序列化。如：`JSON.parse()`函数

## axios

Axios是专注于**网络数据请求**的库。

## 跨域

### 同源策略

如果两个页面的协议、域名和端口都相同，则两个页面具有相同的源。

同源策略（Same Origin Policy）是浏览器提供的一个安全功能

MDN概念：同源策略限制了从同一个源家在的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。（浏览器规定，A网站的JS不允许和非同源的C网站进行资源的交互。）

### 跨域

同源反之即是跨域。

出现跨域的根本原因：浏览器的同源策略不允许非同源的URL之间进行资源的交互。

> 浏览器允许发起跨域请求，但是跨域请求回来的数据会被浏览器拦截，无法被页面获取到。

**如何实现跨域数据请求：**

- JSONP

临时解决方案，只支持GET请求

- CORS

W3C标准，属于跨域Ajax请求到根本解决方案。支持GET和POST请求；确定是不兼容某些低版本的浏览器。

### JSONP

JSON（JSON with Padding）是JSON的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。

**实现原理：**

由于浏览器同源策略的限制，网页中无法通过Ajax请求非同源的借口数据。但是`<script>`标签不受浏览器同源策略的影响，可以通过其src属性请求非同源的js脚本。

JSONP即是通过`<script>`标签的src属性，请求跨域的数据接口，并通过函数调用的形式，接收跨域接口响应回来的数据。

### 防抖

防抖策略（debounce）是当事件被处罚后，延迟n秒后再执行回调，如果在这n秒内时间又被触发，则重新计时。

### 节流

节流策略（throttle）可以减少一段时间内时间的触发频率。

## 网络

### HTTP

通信三要素：
1. 主体
2. 内容
3. 方式

**通信协议**是指通信双方完成通信所必须遵守的规则和约定。

#### HTTP请求消息

客户端发起的请求叫做HTTP请求，客户端发送到服务器的消息，叫做HTTP请求消息。

- 请求行

> 由请求方式、URL和HTTP协议版本3个部分组成，它们之间使用空格隔开。

- 请求头部

> 用来描述客户端的基本信息，从而把客户端相关的信息告知服务器。
> > User-Agent: 说明当前是什么类型的浏览器；
> > Content-Type: 描述发送到服务器的数据格式；
> > Accept: 描述客户端能够接收什么类型的返回内容；
> > Accept-Language: 描述客户端期望接收哪种人类语言的文本内容。

- 空行

> 最后一个请求头字段的后面是一个空行，通知服务器请求头部至此结束。

- 请求体

> 请求体中存放的是要通过POST方式提交到服务器的数据。

**只有POST请求才有请求体，GET请求没有请求体。**

#### HTTP响应消息

响应消息就是服务器响应给客户端的消息内容，也叫响应报文。

- 状态行

> 由HTTP协议版本、状态码和状态码的描述文本组成。

- 响应头部

> 用来描述服务器的基本信息。

- 空行
- 响应体

#### HTTP请求方法

用来表明要对服务器上的资源执行的操作。

#### HTTP响应状态码

HTTP响应状态码（HTTP Status Code）用来标识响应的状态。


