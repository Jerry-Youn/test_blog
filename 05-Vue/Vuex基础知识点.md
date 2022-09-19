## Vuex的价值

Vuex是一个大型的状态管理系统。

> 状态：是指数据。

Vuex的价值

- 



## Vuex的使用步骤

文件位置：main.js

```js
// 1.引入
improt Vuex from 'vuex'
// 2.注册
Vue.use(Vuex)
// 3.实例化
const store = new Vuex.Store()
// 4.挂载
new Vue({
  store,
  .......
})
```



## 概念五：Modules

### state 模块化

#### 第一步：定义

文件位置：

```js
modules:{
  studentA:{
    state:{
      name:AAAA,
      age:25,
      ......
    },
  },
    
  studentB:{
    state:{
      name:BBBB,
      age:20,
      ......
    },
  },
}
```



#### 第二步：使用步骤

文件位置：

```js
modules:{
  .....
},
getters:{
  studentAname:state => state.studentA.name
  studentAage:state => statestudentA.age
  studentBname:state => state.studentB.name
	studentBage:state => statestudentB.age
}
```



文件位置：

```vue
<template>
  <div>
    {{ studentAname }}
    .....
  </div>
</template>

<script>
import {mapGetters} from 'Vuex'

export default {
  compputer:{
    ...mapGetters(['studentAname','studentAage','studentBname','studentBage'])
  }
}
</script>
```



### mutations / actions 模块化

#### 常规用法

- 使用情景：各模块中的mutations / actions 的方法名 **互不相同**。

> 原因：在默认情况下，mutations、actions、getters是注册在全局，全局都可以使用



##### 第一步：定义

```js
modules:{
  studentA:{
    state:{
      name:AAAA,
      age:25,
      ......
    },
    mutations:{
      setStudentAage(state){
        state.age += 2
      }
    }
  },
    
  studentB:{
    state:{
      name:BBBB,
      age:20,
      ......
    },
    mutations:{
      setStudentBage(state){
        state.age += 2
      }
    }
  },
}
```



##### 第二步：步骤

> 各模块的 mutation不重名 / 没有命名空间锁 的情况下。

```vue
<template>
  ....
</template>

<script>
import {mapMutaions} from 'Vuex'

export default {
  methods:{
    ...mapMutations(['setStudentAage','setStudentBage'])
  }
}
</script>
```





#### 异常用法

- 使用情景：各模块中的mutations / actions 的方法名出现 **相同**。



##### 第一步：添加命名空间锁

作用：让该模块的mutation、actions不能够全局调用。

用法：在对应的对应模块中加入`namespaced:true`

```js
modules:{
  studentsA:{
    namespaced:true,
    states:{
      .....
    },
    mutations:{
      setAge(state){
        state.age ++,
      }
    }
  },
    
  studentsB:{
    namespaced:true,
    states:{
      .....
    },
    mutations:{
      setAge(state){
        state.age ++,
      }
    }
  },
}
```



##### 第二步：调用相应模块的方法

###### 方法一：利用commit调用时加上模块路径





###### 方法二：辅助函数加上模块路径(不推荐)





###### 方法三：配置 mapMutations、mapAcitons的时候，加上模块参数





###### 方法四：配置 createNamespacedHelpers































