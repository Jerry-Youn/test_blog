## vm.$options

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

## @mixin和@include

sass官网：https://www.sasscss.com/documentation/at-rules/mixin

比较好的解释：https://blog.csdn.net/qq_39490750/article/details/123844746 

​								https://www.runoob.com/sass/sass-mixin-include.html

人资项目的混入





























