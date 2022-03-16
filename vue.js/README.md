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

## axios

> axios是一个专注于网络请求的库

**基本语法：**

```js
axios({
  method: '请求类型',
  url: '请求地址',
  params: {URL中的查询参数},
  data: {请求体参数}
}).then((result) => {
  //回调函数
  //result 为请求成功后的结果是一个Promise对象
})
```

## 单页面应用程序

> Single Page Application(SPA), 所有的功能与交互都在唯一的页面完成。

### Vue项目的运行流程

> 通过 main.js 将 App.vue 渲染到 index.html 的指定区域中。

- App.vue 用来编写待渲染的模版结构
- index.html 中需要预留一个 el 区域
- main.js 把 App.vue 渲染到了 index.html 所预留的区域中

## 组件

### 组件化开发

> 根据**封装**的思想，把页面上可重用的UI结构封装为组件，从而方便项目的开发和维护。

### 组成

- template： 模版结构
- script： JavaScript 行为
- style： 样式

### 使用步骤

1. 使用 `import` 导入需要的组件

```js
import Left from '@/components/Left.vue'
```

2. 使用 `components` 节点注册组件

```js
export default {
  components: {
    Left
  }
}
```

> 通过 components 注册的是私有子组件。

3. 以标签形式使用刚注册的组件

```html
<Left></Left>
```

**注册全局组件**

在 vue 项目的 main.js 入口文件中， 通过 `Vue.component()` 方法可以注册全局组件。

### 组件的 `props`

`props` 是组件的自定义属性，在封装组件的时候，合理的使用可以极大的提高组件的复用性。

> props 是只读的

`default` 默认值

`type` 值类型

`required` 必填值

### 组件的样式冲突

> 默认情况下， 写在 .vue 组件中的样式会全局生效，因此很容易会造成多个组件之间的样式冲突问题。

可以通过 `scoped` 解决，只在该组件下生效。

`/deep/` 样式穿透

> 使用第三方组件库的时候，如果有修改其默认样式的需求，需要用到 `/deep/`

### 组件的生命周期

> 生命周期是指一个组件从创建 -> 运行 -> 销毁的整个过程，强调的是一个时间段。

生命周期函数： 是由 vue 框架提供的内置函数，会伴随组件的生命周期，自动按次序执行。

![](https://gitee.com/merlinalex/pic-go/raw/master/lifecycle.png)

1. 组件创建阶段

`beforeCreate`

`created`

> 该生命周期函数非常常用，经常在其中调用 methods 中的方法， 请求服务中的数据，并且把请求到的数据转存到 data 中，供 template 模版渲染到时候使用。

`beforeMount`

`mounted`

> 对于 DOM 结构的操作最早在该阶段。

2. 组件运行阶段

`beforeUpdate`

`updated`

3. 组件销毁阶段

`beforeDestroy`

`destroyed`

### 组件之间的数据共享

**父组件 -> 子组件**

需要使用 **自定义属性**

**子组件 -> 父组件**

需要使用 **自定义事件**

**兄弟之间的数据共享**

使用 `EventBus`

## ref引用

> 每个 vue 组件实例上，都包含一个 $refs 对象，里面存储着对应的DOM元素或组件的饮用。默认情况下，组件的 $refs 指向一个空对象。

`this.$nextTick(cb)` 方法会把 cb 回调推迟到下一个 DOM 更新周期之后执行。

## 动态组件 

`<component>` 组件，专门用来实现动态组件的渲染。

使用 `keep-alive` 保持状态： 可以把内部的组件进行缓存，而不是销毁组件。

`keep-alive` 对应的生命周期函数： 

- 被缓存时：`deactivated`函数
- 被激活时：`activated`函数

```html
<keep-alive>
  <component></component>
</keep-alive>
```

可以通过 `include` 指定被缓存的组件。

可以通过 `exclude` 指定不被缓存的组件。

但是不要同时使用 `include` 和 `exclude`

## 插槽

> 插槽（slot）是 vue 为组件的封装者提供的能力。允许开发者在封装组件时，把不确定、希望由用户指定的部分定义为插槽。

```html
<slot></slot>
```

每一个 slot 插槽都要有一个 name 属性， 若省略， 则有一个默认名称 default

`v-slot` 可以指定放在哪个插槽中，但是只能放在 `<template>` 标签上，可以用 `#` 简写。

```html
<template v-slot:default>
  <p></p>
</template>
```

## 自定义指令

### 私有自定义指令

> 每个 vue 组件中， 可以在 directives 节点下声明私有自定义指令。

```js
directives: {
  color: {
    bind(el){
      el.style.color = 'red'
    }
  }
}
```

### 全局自定义指令

通过 `Vue.directives()` 创建

## 路由

> 路由就是对应关系

**前端路由：** Hash 地址与组件之间的对应关系

**前端路由的工作方式：** 

1. 用户点击了页面上的路由链接
2. URL地址栏中的 Hash 值发生了变化
3. 前端路由监听到了 Hash 地址的变化
4. 前端路由把当前 Hash 地址对应的组件渲染到浏览器中

### `vue-router` 

1. 安装

```bash
npm i vue-router -S
```

2. 创建路由模块

在 src/ 目录下创建 router/index.js

3. 导入并挂载路由模块

`router/index.js`

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const router = new VueRouter()

export default router
```

`main.js`

```js
import router from '@/router/index.js'

// ................................

new Vue ({
  //...

  router
}).$mount('#app')
```

4. 声明路由链接和占位符

```html

<!-- 路由占位符 -->
<router-view></router-view>
```

### 路由重定向

> 用户在访问 A 的时候，强制用户调转到 C， 从而展示特定的组件页面。

```js
const router = new VueRouter({
  routes: [
    { path: '/', redirect: '/home' }
  ]
})
```

### 嵌套路由

> 通过路由实现组件的嵌套展示。

**通过 children 属性声明子路由规则**

```js
const router = new VueRouter({
  routes: [
    {
      path: '/about',
      component: About,
      children: [
        { path: 'tab1', component: Tab1 },
        { path: 'tab2', component: Tab2 }
      ]
    }
  ]
})
```

**默认子路由：**若某个路由规则的 path 值为空字符串，则该条路由规则叫做“默认子路由”

### 动态路由匹配

> 把 Hash 地址中可变的部分定义为参数项，从而提高路由规则的复用性。

### 导航

点击链接实现导航的方式，叫做声明式导航；调用 API 方法实现导航的方式，叫做编程式导航。

`this.$router.push('hash')`

- 跳转到指定的 hash 地址，并增加一条历史记录

`this.$router.replace('hash')`

- 跳转到指定的 hash 地址，并替换当前的历史记录 

`this.$router.go(n)`

- 可以在浏览历史中前进后退

**导航守卫：** 可以控制路由的访问权限。

**全局前置守卫**

每次发生路由的导航跳转时，都会触发全局前置守卫

```js
const router = new VueRouter({})

router.beforeEach((to, from, next) => {
  // to 将要访问的路由
  // from 将要离开的路由 
  // next 函数，调用 next() 表示放行，允许这次路由导航
})
```

![](https://gitee.com/merlinalex/pic-go/raw/master/20220316170726.png)