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

|          | 超小屏幕 | 小屏幕   | 中等屏幕 | 大屏幕   |
| :------- | :------- | :------- | :------- | :------- |
| 响应断点 | <768px   | >=768px  | >=992px  | >=1200px |
| 别名     | xs       | sm       | md       | lg       |
| 容器宽度 | 100%     | 750px    | 970px    | 1170px   |
| 类前缀   | col-xs-* | col-sm-* | col-md-* | col-lg-* |
| 列数     | 12       | 12       | 12       | 12       |
| 列间隙   | 30px     | 30px     | 30px     | 30px     |

`.container` 默认指定宽度且居中

`.container-fluid` 宽度均为100%

