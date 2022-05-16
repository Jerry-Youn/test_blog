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

`<h1>标签`普通组件的写法：

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

`<h1>标签`render函数的写法:

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

## @mixin和@include

sass官网：https://www.sasscss.com/documentation/at-rules/mixin

比较好的解释：https://blog.csdn.net/qq_39490750/article/details/123844746 

​								https://www.runoob.com/sass/sass-mixin-include.html

人资项目的混入

















