# <center>Vue.js

## 前端工程化

- 模块化
- 组件化
- 规范化
- 自动化

> 在企业级的前端开发中，把前端开发需要的工具、技术、流程、经验等进行规范化、标准化。

## webpack

> webpack是前端项目工程化的具体解决方案。

**主要功能：**

提供了友好的前端模块化开发支持，以及代码压缩混淆、处理浏览器端JavaScript的兼容性、性能优化等强大的功能。

**安装：**

```bash
npm i webpack webpack-cli -D
```

**配置：**

`webpack.config.js`

```js
module.exports = {
  mode: 'development' or 'production'
}
```

`package.json`

```js
"scripts": {
  "dev": "webpack"
}
```

**默认约定：**

打包入口：src -> index.js

输出路径：dist -> main.js

可以在`webpack.config.js`中修改 

通过`entry`节点指定打包的入口，通过`output`节点制定打包的出口。

```js
module.exports = {
  entry: path,
  output: {
    path: path,
    filename: 'name'
  }
}
```

### webpack 的插件

**`webpack-dev-server`**

当修改了源代码，webpack会自动进行项目的打包和构建。

**配置：**

`package.json`

```js
"scripts": {
  "dev": "webpack serve"
}
```

`webpack.config.js`

```js
module.exports = {
  devServer: {
    open: true, //初次打包完成后，自动打开浏览器
    host: '127.0.0.1', //地址
    port: 80
  }
}
```

**`html-webpack-plugin`**

可以自定制`index.html`页面的内容

**配置：**

`webpack.config.js`

```js
const HtmlPlugin = require('html-webpack-plugin')

const htmlPlugin = new HtmlPlugin({
  template: '源文件',
  filename: '生成文件',
})

module.exports = {
  mode: 'development',
  plugins: [htmlPlugin]
}
```

### webpack的loader

webpack默认只能处理.js后缀名结尾的模块。其他的模块则需要调用loader加载起才能正常打包。

> 协助webpack打包处理特定的文件模块。

- css-loader: 可以打包处理.css文件
- less-loader: 可以打包处理.less文件
- babel-loader: 可以打包处理webpack无法处理的高级JS语法


**配置：**

`webpack.config.js`

```js
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: ['style-loader', 'css-loader']}
    ]
  }
}
```

### SourceMap

SourceMap即位置文件，存储着位置信息。

**开发环境：**

`webpack.config.js`

```js
module.exports = {
  devtool: 'eval-source-map'
}
```

**生产环境：**

出于安全考虑应关闭SourceMap。

如果只想定位报错的具体行数，而不想暴露源码。可以将`devtool`的值设置为`nosources-source-map`。

## Vue简介

> Vue是一套用于构建用户界面的前端框架。

### 特性

#### 数据驱动视图

在使用了vue的页面中，vue会监听数据的变化，从而自动重新渲染页面的结构。

**好处：**

当页面数据发生变化时，页面会自动重新渲染。

*数据驱动视图是单向的数据绑定*

#### 双向数据绑定

在填写表单时，双向数据绑定可以辅助开发者在不操作DOM的前提下，自动把用户填写的内容同步到数据源中。

**好处：**

开发者不再需要手动操作DOM元素来获取表单最新的值。

### MVVM

> MVVM是vue实现数据驱动视图和双向数据绑定的核心原理。

- Model 当前页面渲染时所依赖的数据源
- View 当前页面所渲染的DOM结构
- ViewModel vue实例，是MVVM的核心

## vue的基本使用

```js
<script>
    // 创建Vue实例对象
  const vm = new Vue({
    // 表示当前的vm控制页面的区域
    el: '#app',
    // 要渲染到页面上的数据
    data: {
      username: 'mike'
    }
  })
</script>
```

## vue指令

> 指令是vue为开发者提供的模版语法，用于辅助开发者渲染页面的基本结构。

1. 内容渲染指令
2. 属性绑定指令
3. 事件绑定指令
4. 双向绑定指令
5. 条件渲染指令
6. 列表渲染指令

### 内容渲染指令

- v-text

> 渲染DOM元素的文本内容
> 
> 缺点：会覆盖元素内部原有的内容

- {{}}(插值表达式)
- v-html

> 可以把带有标签的字符串，渲染成真正的HTML页面

### 属性绑定指令

插值表达式只能用在元素的内容节点上，不能用在元素节点上。

`v-bind`属性绑定指令

可以简写为`:`

### 事件绑定指令

`v-on`事件绑定指令，可以用来为DOM元素绑定事件监听。可以简写为`@`

> `methods`用来绑定事件处理函数。

在处理函数中，`this === vm`

事件处理函数默认有事件对象e，但如果主动为该事件处理函数传参的话，就会覆盖e。vue提供了内置变量，`$event`

**按键修饰符：** `@keyup`在监听键盘事件的时候，可以为键盘相关的事件添加键盘修饰符来判断按键。

### 双向绑定指令

`v-model` 双向绑定指令可以用来辅助在不操作DOM的前提下，快速获取表单数据。

**修饰符：**

1. `.number`: 自动讲用户的输入值转为数值类型
2. `.trim`: 自动过滤用户输入的首尾空白字符
3. `.lazy`: 在change时而非input时更新

### 条件渲染指令

用来按需控制DOM的显示于隐藏

`v-if`： 直接移除

`v-show`： 使用 `style display:none` 隐藏

如果需要频繁的切换元素的显示状态，`v-show`性能更好;
如果刚进入页面的时候某些元素默认不需要被展示，且后期该元素也可能不需要被展示出来，此时`v-if`性能会更好

`v-else(-if)`: 需要配合 `v-if` 进行使用。

### 列表渲染指令

`v-for`: 基于一个数组来循环渲染一个列表结构。 `v-for` 指令需要使用 **item in items** 形式的特殊语法。

- items是带循环的数组
- item是被循环的每一项

可选项： `(item, index) in items`

index表示当前项的索引, 从零开始。

建议只要用到了 `v-for` 指令，那么需要绑定一个 `:key` 属性，且一般使用id为key值,key只能是数值或字符串，key值不能重复。

```html
<tr v-for="item in items" :key="item.id"></tr>
```

## 过滤器（Vue3中已被移除）

> 常用于文本的格式化，可以用在 **插值表达式** 和 **`v-bind` 属性绑定**

过滤器应该被添加在JavaScript表达式的尾部，由”管道符“进行调用。

过滤器必须被定义到 filters 节点下，其本质是一个函数且必须有返回值。

可以使用 `Vue.filter` 定义全局过滤器。

## 侦听器

> 允许开发者监视数据的变化，从而针对数据的变化做特定的操作。

1. 方法格式的侦听器
  - 缺点： 无法在刚进入页面时，自动触发。
  - 缺点： 如果侦听的是一个对象，如果对象中的属性发生了变化，并不会触发侦听器。

```js
watch: {
  username (newVal, oldVal) {
    console.log(newVal, oldVal)
  }
}
```
2. 对象格式的侦听器
  - 好处： 可以通过 **immediate** 选项，让侦听器自动触发。
  - 好处： 可以通过 **deep** 选项， 让侦听器深度监听对象中的每个属性的变化。

```js
watch: {
  username: {
    handler () {
      console.log(newVal, oldVal)
    },
    immediate: true
  }
}
```

## 计算属性

> 指通过一系列运算之后，最终得到一个属性值
> 
> 这个动态计算出来的属性值可以被模版结构或methods方法使用。

需定义到 `computed` 节点之下

计算属性在定义的时候，要定义成“方法格式”；使用的时候当成普通的属性使用即可。

**好处：** 

1. 实现了代码的复用。
2. 只要计算属性中依赖的数据源变化了，则计算属性会自动重新要求值。
