## 「如何理解前端语义化？」

1. ###### 让人更容易读懂，有利于构建清晰的代码框架（增加代码的可读性）

2. ###### 让搜索引擎更容易读懂（SEO）



## 「常用的语义化标签有哪些？」

➤ html5之前

`h1~h6 p br ul ol li dl dt dd em strong table thead tobdy tfoot td th caption`

注意的点：

- `b`、`font`、`u`等纯样式标签不要使用
- `strong`是为了强调重要而加粗（不要用`b`，`b`是为了加粗而加粗），`em`是斜体是强调（不用`i` ，`i`就是斜体）
- 每个`input`标签对应的说明文本都需要使用`label`标签
- 表单域要使用`fieldset`包起来，并使用`legend`说明表单的用途

➤ html5新增

`header footer nav aside section artice`



## 「块状元素&内联元素？」

➤ 块级元素 :

`ul li ol dl dd dt table h1-h6 form ` 等等

➤ 内联元素 ：

` span b img input button` 等等

➤ 样式转换：

- `display:block` 行内元素转换为块级元素
- `display:inline` 块级元素转换为行内元素
- `display:inline-block` 转为内联元素



## 「盒子模型的宽度计算」

➤ 标准盒子模型

默认 `box-sizing : content-box`

```html
#box {
	width : 20px;
	padding : 20px;
	margin : 20px;
	border : 2px solid #ccc;
}
```

> offsetWidth : 包括 width + border + padding
>
> 所以这里的offsetwidth是：64px

➤ 弹性盒子模型

盒模型 `box-sizing：border-box`

```html
#box {
	width : 80px;
	padding : 20px;
	margin : 20px;
	border : 2px solid #ccc;
	box-sizing : border-box;
}
```

> 这里的offsetwidth是：80px
>
> 如果padding + border 的宽度大于 width，这个时候的offsetWidth 就是 padding + border了



## 「margin」

➤ margin的折叠问题

```html
<style>
      p {
        font-size: 16px;
        margin-top: 20px;
        margin-bottom: 10px;
        line-height: 1;
      }
</style>
<body>
    <p>第一行</p>
    <p></p>
    <p></p>
    <p>末行</p>
</body>
```

> 最后一行和 第一行之间的距离是 `20px`

计算方法:

- 全部都为正值，取最大者；
- 不全是正值，则都取绝对值，然后用正值的最大值减去绝对值的最大值；

➤ margin的负值问题

- margin-left、margib-top的负值都是自身元素向左边、上面移动。
- margin-right的负值是目标元素的右边元素向右移动。
- margin-bottom的负值是目标元素的下面元素向上移动。



## 「BFC：块级格式化上下文」

- 概念
  - BFC是一个完全独立的空间（一块独立的渲染区域），让空间里的子元素不会影响到外面的布局
- BFC规则
  - `BFC`就是一个块级元素，块级元素会在垂直方向一个接一个的排列
  - `BFC`就是页面中的一个隔离的独立容器，容器里的标签不会影响到外部标签
  - 垂直方向的距离由margin决定， 属于同一个`BFC`的两个相邻的标签外边距会发生重叠
  - 计算`BFC`的高度时，浮动元素也参与计算
- 形成bfc常见条件：
  - `float` 不为 `none`
  - `position` 为 `absolute` `fixed`
  - `overflow` 不是 `visible`
  - `display` 为 `flex` `inline-block` `table-cell`等
- 常用情景：
  - 清除浮动
  - margin重叠



## 「float布局」

- 圣杯布局和双飞翼布局的目的
  - 三栏布局，中间一栏最先加载和渲染（内容最重要）
  - 两侧内容固定，中间内容随着宽度自适应
  - 一般用于PC网页

- 圣杯布局和双飞翼布局的总结
  - 使用float布局
  - 两侧使用margin负值，以便和中间内容横向重叠
  - 防止中间内容被两侧覆盖，一个用padding，一个用margin





















