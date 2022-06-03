# Vue介绍

## Vue的安装

方法一：直接用`<script>`引入，`Vue` 会被注册为一个全局变量。

> 可以引入`vue.js`文件 或者 cdn

## 声明式渲染



# 渲染函数--render

## 基础

> 主要依靠`createElement`函数实现。

想要实现的效果：

```html
<h1>
  <a name="hello-world" href="#hello-world">
    Hello world!
  </a>
</h1>
```

`<h1>标签` 普通组件的写法：

```javascript
<script type="text/x-template" id="anchored-heading-template">
  <h1 v-if="level === 1">
    <slot></slot>
  </h1>
  <h2 v-else-if="level === 2">
    <slot></slot>
  </h2>
  ···
  ···
  <h6 v-else-if="level === 6">
    <slot></slot>
  </h6>
</script>

//注册组件
<script>
 Vue.component('anchored-heading', {
   template: '#anchored-heading-template', //注册组件的id
   props: {
     level: {
       type: Number,
       required: true
     }
   }
 })
</script>
```

`<h1>标签` render函数的写法:

```js
Vue.component('anchored-heading', {
  render: function (createElement) {
    return createElement(
      'h' + this.level,   // 标签名称
      this.$slots.default // 子节点数组
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```

## 使用JavaScript代替模板功能

### # v-if 和 v-for

实现效果：

```html
<ul v-if="items.length">
  <li v-for="item in items">{{ item.name }}</li>
</ul>
<p v-else>No items found.</p>
```

这些都可以在渲染函数中用 JavaScript 的 `if`/`else` 和 `map` 来重写：

```js
props: ['items'],
render: function (createElement) {
  if (this.items.length) {
    return createElement('ul', this.items.map(function (item) {
      return createElement('li', item.name)
    }))
  } else {
    return createElement('p', 'No items found.')
  }
}
```

## createElement 参数

```js
createElement(
  	// {String | Object | Function}
  	// 一个 HTML 标签名、组件选项对象，或者
  	// resolve 了上述任何一种的一个 async 函数。【必填项】。
  'div',

  	// {Object}
  	// 一个与模板中 attribute 对应的数据对象。【可选】
  {
    下面会深入讲解。
  },

  	// {String | Array}
  	// 子级虚拟节点 (VNodes)，由 `createElement()` 构建而成，
  	// 也可以使用字符串来生成“文本虚拟节点”。【可选】
  [
    '先写一些文字',
    createElement('h1', '一则头条'),
    createElement(MyComponent, {
      props: {
        someProp: 'foobar'
      }
    })
  ]
)
```

### # 深入数据对象

```js
{
  	// 与 `v-bind:class` 的 API 相同，
  	// 接受一个字符串、对象或字符串和对象组成的数组
  'class': {
    foo: true,
    bar: false
  },
    
  	// 与 `v-bind:style` 的 API 相同，
  	// 接受一个字符串、对象，或对象组成的数组
  style: {
    color: 'red',
    fontSize: '14px'
  },
    
  	// 普通的 HTML attribute
  attrs: {
    id: 'foo'
  },
    
  	// 组件 prop
  props: {
    myProp: 'bar'
  },
    
  	// DOM property
  domProps: {
    innerHTML: 'baz'
  },
    
  	// 事件监听器在 `on` 内，
  	// 但不再支持如 `v-on:keyup.enter` 这样的修饰器。
  	// 需要在处理函数中手动检查 keyCode。
  on: {
    click: this.clickHandler
  },
    
  	// 仅用于组件，用于监听原生事件，而不是组件内部使用
  	// `vm.$emit` 触发的事件。
  nativeOn: {
    click: this.nativeClickHandler
  },
    
  	// 自定义指令。注意，你无法对 `binding` 中的 `oldValue`
  	// 赋值，因为 Vue 已经自动为你进行了同步。
  directives: [
    {
      name: 'my-custom-directive',
      value: '2',
      expression: '1 + 1',
      arg: 'foo',
      modifiers: {
        bar: true
      }
    }
  ],
  	// 作用域插槽的格式为
  	// { name: props => VNode | Array<VNode> }
  scopedSlots: {
    default: props => createElement('span', props.text)
  },
    
  // 如果组件是其它组件的子组件，需为插槽指定名称
  slot: 'name-of-slot',
    
  // 其它特殊顶层 property
  key: 'myKey',
  ref: 'myRef',
    
  // 如果你在渲染函数中给多个元素都应用了相同的 ref 名，
  // 那么 `$refs.myRef` 会变成一个数组。
  refInFor: true
}
```

### # 完整示例

```js
Vue.component('anchored-heading', {
  render: function (createElement) {
    return createElement(
      'h' + this.level,
      [
        createElement('a', {
          attrs: {
            name: 自定义,
            href: '#' + 自定义
          }
        }, this.$slots.default)
      ]
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```



# vm.$options

作用：用来 **获取/增加** 定义在data外的自定义属性（包括函数）

开发场景：用来获取距离组件最近的父组件。（例如`el-from-item`获取`el-from`；`el-col`获取`el-row`）

语法：

> 语法1：`this.$options['自定义属性名']`
>
> 语法2：`this.$options.自定义属性名`

代码展示

```vue
<script>
export default {
  name: "zs",
  age: 12,
  haha() {
    console.log("haha");
  },
  data() {
    return {
    };
  },
  created() {  
    console.log(this.$options.name);  // zs
    console.log(this.$options.age);  //12
    this.$options.haha();  // haha
    this.$options.myoption = '888888'
    console.log(this.$options.myoption);  //888888
  },
}
</script>
```



# sass

## sass简介

1. Sass 扩展了 CSS3，增加了规则、变量、混入、选择器、继承等等特性，使它的语法内部可以使用动态变量等，所以它更像一种极简单的动态语言。
2. Sass 生成良好格式化的 CSS 代码，易于组织和维护。



## 文件扩展名.sass与.scss的区别

- sass
  - 多行注释 / 单行注释 注释符号不必首尾呼应，只需缩进即可。
  - 代码部分
    - 缩进式语法
    - 代码末端不需要写 `；` 。
    - 引入文件不需要写双引号。
    - 定义混入用 `=` 代替 `@mixin`，引用混入用 `+`  代替 `@include`

sass代码展示：

```scss
@import base

//混入
=alter 
  color: #000
  background: #fff
  
.alert-warning
  +alert //引用混入。
  
ul
  font-size:16px
  li
  	list-style:none
```



- scss
  - 多行注释需要首尾呼应
  - 代码部分
    - 嵌套式语法。
    - 其他与sass相反。

scss代码展示：

```scss
@improt "base";

@mixin alert {
  color: red;
  background: #000;
}

.alert-warning {
  @unclude alert;
}

ul {
  font-size:16px;
  li {
    list-style:none;
  }
} 
```



## 变量

- 定义变量：`$ 变量名:属性值` ；  使用变量：`$变量名` 。
- 变量也可以套娃，比如我定义一个变量名为 `$cxk`，里面引用了 `$rapper`。

代码展示：

```scss
$ rapper:red;
$ cxk:1px soild $rapper;
```



## 嵌套

注意：

- 使用伪类选择器的时候，必须用上 `&` 符号。否则样式效果就会不生效。
- 使用 ` —` 符号定义的样式名字，也可以使用  `&` 符号进行衔接嵌套。
- 属性也可以写嵌套。

嵌套代码展示：

```scss
.dataList {
  li {
    height: 20px;
    width: 100px;
    background-color: red;
    margin-bottom: 5px;
    // 相当于：.dataList li:hover{}
    &:hover {
      background-color: green;
    }
  }
  // 相当于：.dataList-aaa{ }
  & &-aaa {
    height: 20px;
    width: 100px;
    background-color: orange;
  }
}
```

属性嵌套代码展示：

```scss
div{
  height:100px;
  font:{
    family:'weiruanyahei';
    size:20px;
    weight:700;
  }
}

//相当于
div{
  height:100px;
  font-family:'weiruanyahei';
  font-size:20px;
  font-weight:700
}
```



## 混入 @mixin

### 常见用法

定义混入：

```
@mixin 变量名（参数1(可省略)，参数2...）{ 
	...样式...
}
```

使用混入： `@include 变量名`

> 代码展示：
>

```scss
@mixin alter($text-color,$background-color){
  color:$text-color;
  background-color:$background-color;
}

.dataList {
  @include alter(#fff,#000); //或者可以通过给制定参数赋值(此时可以不用在意顺序)，
  													 //即 @include alter($background-color：#000，$text-color：#fff)
}
```

> 相当于：
>

```
.dataList {
  color: #fff;
  background-color: #000;
}
```

其他参考：https://www.runoob.com/sass/sass-mixin-include.html

### 拓展1

- ###### 想要在混入中定义样式，配合`@content`和`#{$变量名}`使用。

> 代码展示：

```scss
【A文件（定义混入）】
@mixin b($block) {
  //其中 $namespace=el
  $B: $namespace+'-'+$block !global;

  .#{$B} {
    @content;
  }
}

【B文件（使用混入）】
@include b(row) {
  position: relative;
  box-sizing: border-box;
  @include utils-clearfix;
}
```

> 相当于：

```scss
.el-row{
  position: relative;
  box-sizing: border-box;
}
```



### 拓展2

- `@at-root`的作用：让后面的样式跳出目前层级到顶层。即调用子元素的样式时，外面不需要再包一层父元素的盒子。

> 代码展示：

```scss
【A文件（定义混入）】
@mixin m($变量1) {
  ....

  @at-root {
   #{$变量2} {
      @content;
    }
  }
}

【B文件（使用混入）】
.el-row{
  ....

  @include m(flex) {
   ....
  }
}
```

> 相当于

```html
<div class="el-row el-row--flex">我爱打代码</div>
```





## 继承 @extend

- 定义用法：`@extend 变量名`

代码展示：

```scss
.alter{
  color: #fff;
}

.datalist{
  @extend .alter;
  background-color: #000;
}
```

相当于：

```scss
.alter, .datalist{
  color: #fff;
}

.datalist{
  background-color: #000;
}
```



## 引入 @import

- 定义用法：`@import: “…路径”;`

> 注意：引入一个`.scss`后缀的文件作为自己的一部分，被引入的那个文件并不会转换成`.css`格式的，所以此文件命名要注意以下划线开头，如：`_base.scss` ，引入它的时候不用写下划线。

代码展示：

```scss
建立一个文件叫 _base.scss，里面写上一些选择器和样式。

另外一个文件中引入：@import: "base";
```



## 计算

- 可以使用 `（ ）`  来提高运算的优先级。
- 单位不可以重复。



## @if

- 定义语法：

```scss
@if 判断语句 {
  ...样式...;
}@else if 判断语句{
  ...样式...;
}@else{
  ...样式...;
}
```

代码示范：

```scss
$theme: "dark";

.themeColor{
  @if $theme == dark {
    background-color: black;
  }@else if $theme ==light {
    background-color: white;
  }#else{
    background-color: grey;
  }
}
```

相当于：

```scss
.themeColor{
  background-color: black;
}
```



## @for

- 定义用法：

```scss
方法一（结束值执行）：
// 结束值 或者 开始值 都可以用变量控制。
@for $变量名 from 开始值 through 结束值{
  ...样式...
}

方法二（结束值不执行）：
@for 变量名 from 开始值 to 结束值{
  ...样式...
}
```

代码展示：

```scss
$colimns:4;

@for $i from 1 through $colimns {
  .col-#{$i} {
    width:100%/$colimns*$i;
  }
}
```

输出结果：

```scss
.col-1{
  width:25%;
}
.col-2{
  width:50%;
}
.col-3{
  width:75%;
}
.col-4{
  width:100%;
}
```



## @each

- 定义用法：

```scss
$变量名：参数1 参数2 参数3 ....；

@each $key in $变量名 {
  ..样式..
}
```

代码展示：

```scss
$color: red green grey;

@each $key in $color {
  .box-#{$key}{
    color:$key;
  }
}
```

相当于：

```scss
.box-red {
	color:red;
}
.box-green {
  color:green;
}
.box-grey {
  color:grey;
}
```



## @while

- 定义用法：

```scss
@while 条件 {
  ...样式...
}
```

代码展示

```scss
$get
@while $get<3 {
   .box-#{$get}{
    height:$get*1px;
  }
  $get:$get+1;
}
```

相当于：

```scss
.box-1{
  height: 1px;
}

.box-2{
  height: 2px;
}
```





## 自定义函数

- 定义用法：

```scss
@function 名字(参数1，参数2，....){
  ..样式..
}
```

代码展示：

```scss
$colors:(light:#fff , dark:#000);

@function colorFn($key){
  @return map-get($colors,$key);
}

body{
  background-color:colorFn(light);
}
```

相当于：

```scss
body{
  background-color:#fff;
}
```



# el-row组件

## 知识点

1. css的命名规范

   > - 组件名在在前，比如“el-input”。
   > - 组件的子元素用两个下划线，比如“el-input__inner”。
   > - 修饰符会接到最后用两个中横线隔开，比如：“el-input--success”.
   > - 表示状态的样式命名，加上前缀 "is-"，比如：“is-disabled”

2. render函数

   语法：`render: function (createElement, context) {}`

3. 所有我们写的vue选项都会被放在vue实例属性$options中。比如：在组件中写下 `componentName: 'Elrow'`，我们可以通过`this.$options.componentName`获取到这个选项。

4. 渲染函数`render(h)`中的h这代表creatElement函数。





























