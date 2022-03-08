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

