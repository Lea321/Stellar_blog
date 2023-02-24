---
title: Vue2.0笔记
tags:
  - 笔记
categories: 学习笔记
date: 2022-03-12 22:00:00
updated: 2022-03-12 22:00:00
---

## vue2.0

### vue 指令

#### 1. 内容渲染指令

1. `v-text` 指令的缺点：会覆盖元素内部原有的内容！
2. `{{ }}` 插值表达式：在实际开发中用的最多，只是内容的占位符，不会覆盖原有的内容！
3. `v-html` 指令的作用：可以把带有标签的字符串，渲染成真正的 HTML 内容！
<!-- more -->
**v-text示例**

```js
<!-- 把demo对应的值渲染到p标签中 -->
<p v-text="demo"></p>

<!-- demo1的值会覆盖掉"测试" -->
<p v-text="demo1">测试</p>
```



#### 2. 属性绑定指令

>  注意：插值表达式只能用在元素的**内容节点**中，不能用在元素的**属性节点**中！

+ 在 vue 中，可以使用 `v-bind:` 指令，为元素的属性动态绑定值；

+ 简写是英文的 `:`

+ 在使用 v-bind 属性绑定期间，如果绑定内容需要进行动态拼接，则字符串的外面应该包裹单引号，例如：

  ```js
  <div :title="'box' + index">这是一个 div</div>
  ```



#### 3. 事件绑定指令

1. `v-on:` 简写是 `@`

1. 通过 v-on 绑定的事件处理函数，需要在 methods 节点中进行声明

2. 语法格式为：

   ```js
   <button @click="add"></button>
   
   methods: {
      add() {
   			// 如果在方法中要修改 data 中的数据，可以通过 this 访问到
   			this.count += 1
      }
   }
   ```

3. `$event` 的应用场景：如果默认的事件对象 e 被覆盖了，则可以手动传递一个  $event。例如：

   ```js
   <button @click="add(3, $event)"></button>
   
   methods: {
      add(n, e) {
   			// 如果在方法中要修改 data 中的数据，可以通过 this 访问到
   			this.count += 1
      }
   }
   ```

4. 事件修饰符：

   + `.prevent`  阻止默认行为

     ```js
     <a @click.prevent="xxx">链接</a>
     ```

   + `.stop `  阻止事件冒泡

     ```js
     <button @click.stop="xxx">按钮</button>
     ```

   + `.capture`  以捕获模式触发当前的事件处理函数
   
   + `.once`  绑定的事件只触发1次
   
6. 按键修饰符

   在监听键盘事件时，我们经常需要判断详细的按键。此时，可以为键盘相关的事件添加按键修饰符，例如：

   ```js
   <input @keyup.enter="submit">
   <input @keyup.esc="clear">
   ```

#### 4. v-model 指令

**vue 提供了 v-model 双向数据绑定指令，用来辅助开发者在不操作 DOM 的前提下，快速获取表单的数据。**

1. input 输入框
   + type="radio"
   + type="checkbox"
   + type="xxxx"
2. textarea
3. select

**为了方便对用户输入的内容进行处理，vue 为 v-model 指令提供了 3 个修饰符，分别是：**

| 修饰符  | 作用                           | 示例                            |
| ------- | ------------------------------ | ------------------------------- |
| .number | 自动将用户的输入值转为数值类型 | &lt; input v-model.number="age" &gt; |
| .trim   | 自动过滤用户输入的首尾空白字符 | &lt; input v-model.trim="msg" &gt; |
| .lazy   | 在“change”时而非“input”时更新  | &lt; input v-model.lazy="msg" &gt; |



#### 5. 条件渲染指令

**条件渲染指令用来辅助开发者按需控制 DOM 的显示与隐藏。条件渲染指令有如下两个，分别是：**

1. `v-show` 的原理是：动态为元素添加或移除 `display: none` 样式，来实现元素的显示和隐藏
   + 如果要频繁的切换元素的显示状态，用 v-show 性能会更好
2. `v-if` 的原理是：每次动态创建或移除元素，实现元素的显示和隐藏
   + 如果刚进入页面的时候，某些元素默认不需要被展示，而且后期这个元素很可能也不需要被展示出来，此时 v-if 性能更好

>  在实际开发中，绝大多数情况，不用考虑性能问题，直接使用 v-if 就好了！！！



v-if 指令在使用的时候，有两种方式：

1. 直接给定一个布尔值 true 或 false

   ```js
   <p v-if="true">被 v-if 控制的元素</p>
   ```

2. 给 v-if 提供一个判断条件，根据判断的结果是 true 或 false，来控制元素的显示和隐藏

   ```js
   <p v-if="type === 'A'">良好</p>
   ```

> **v-if** 可以配合 **v-else** 和 **v-else-if** 使用



#### 6. 列表渲染指令

vue 提供了 v-for 列表渲染指令，用来辅助开发者基于一个数组来循环渲染一个列表结构。v-for 指令需要使 用 item in items 形式的特殊语法，其中： 

- items 是待循环的数组 
- item 是被循环的每一项

**v-for 中的索引**

v-for 指令还支持一个可选的第二个参数，即当前项的索引。

语法格式为 (item, index) in items，示例代码如下：

```js
v-for="(item, index) in list"
```

**使用 v-for 建议为每项提供一个唯一的 key 属性**

**key 的注意事项** 

+ key 的值只能是字符串或数字类型 
+ key 的值必须具有唯一性（即：key 的值不能重复） 
+ 建议把数据项 id 属性的值作为 key 的值（因为 id 属性的值具有唯一性） 
+ 使用 index 的值当作 key 的值没有任何意义（因为 index 的值不具有唯一性） 
+ 建议使用 v-for 指令时一定要指定 key 的值（既提升性能、又防止列表状态紊乱）



### 过滤器

+ 过滤器（Filters）是 vue 为开发者提供的功能，常用于文本的格式化。

+ 过滤器可以用在两个地方：**插值表达式** 和 **v-bind** 属性绑定。 

+ 过滤器应该被添加在 JavaScript 表达式的尾部，由“管道符”进行调用。

+ 在创建 vue 实例期间，可以在 **filters** 节点中定义过滤器。

+ 过滤器可以串联地进行调用，通过多个管道符链接。
+ 可以使用 `vue.filter()` 定义全局过滤器
+ 过滤器可以传递参数



**示例代码如下：**

```js
<!-- 管道符的前面是需要处理的值，后面是过滤器函数 -->
<p>{{ message | func }}</p>
<div :id="mid | formatid"></div>
```



#### 过滤器的注意点

1. 要定义到 filters 节点下，**本质是一个函数**
2. 在过滤器函数中，**一定要有 return 值**
3. 在过滤器的形参中，可以获取到“管道符”前面待处理的那个值
4. 如果全局过滤器和私有过滤器名字一致，此时按照“**就近原则**”，调用的是”私有过滤器“



### watch 侦听器

#### 侦听器的格式

1. 方法格式的侦听器

   + 缺点1：无法在刚进入页面的时候，自动触发！！！
   + 缺点2：如果侦听的是一个对象，如果对象中的属性发生了变化，不会触发侦听器！！！

2. 对象格式的侦听器

   + 好处1：可以通过 **immediate** 选项，让侦听器自动触发！！！

   + 好处2：可以通过 **deep** 选项，让侦听器深度监听对象中每个属性的变化！！！

   + > 注意：对象格式的侦听器里面函数名必须是handel，否则会报错。
     >
     > ```js
     > watch: {
     >   // handler 是固定写法，表示当 username 的值变化时，自动调用 handler 处理函数
     >   username: {
     >     handler(n, o) {
     >       console.log(n, o);
     >     },
     >     // 表示页面初次渲染好之后，就立即触发当前的 watch 侦听器
     >     immediate: true
     >   }
     > }
     > ```

3. 如果要侦听的是对象的子属性变化，则必须包裹一层单引号

   ```js
   'user.username'(){}
   ```




### 计算属性

特点：

1. 虽然计算属性在声明的时候被定义为方法，但是计算属性的本质是一个属性 
1. 计算属性会缓存计算的结果，只有计算属性依赖的数据变化时，才会重新进行运算

好处：

1. 实现了代码的复用
2. 只要计算属性中依赖的数据源变化了，则计算属性会自动重新求值！



### axios

> axios 是一个专注于网络请求的库！

#### axios 的基本使用

1. 发起 GET 请求：

   ```js
   axios({
     // 请求方式
     method: 'GET',
     // 请求的地址
     url: 'http://www.liulongbin.top:3006/api/getbooks',
     // URL 中的查询参数
     params: {
       id: 1
     }
   }).then(function (result) {
     console.log(result)
   })
   ```

2. 发起 POST 请求：

   ```js
   document.querySelector('#btnPost').addEventListener('click', async function () {
     // 如果调用某个方法的返回值是 Promise 实例，则前面可以添加 await！
     // await 只能用在被 async “修饰”的方法中
     const { data: res } = await axios({ // 解构赋值使用：进行重命名
       method: 'POST', 
       url: 'http://www.liulongbin.top:3006/api/post',
       data: {
         name: 'zs',
         age: 20
       }
     })
   
     console.log(res)
   })
   ```



### vue-cli 的使用

1. 安装和使用

   ```bash
   安装cli：npm install -g @vue/cli
   创建项目：vue cerate 项目的名称
   ```

2. vue 项目中 src 目录的构成：

   - assets 文件夹：存放项目中用到的静态资源文件，例如：css 样式表、图片资源
   - components 文件夹：程序员封装的、可复用的组件，都要放到 components 目录下
   - main.js 是项目的入口文件。整个项目的运行，要先执行 main.js
   - App.vue 是项目的根组件。

### vue组件

vue 中规定：组件的后缀名是 .vue。之前接触到的 App.vue 文件本质上就是一个 vue 的组件。

每个 .vue 组件都由 3 部分构成，分别是： 

- **template** -> 组件的模板结构 

- script -> 组件的 JavaScript 行为 

- style -> 组件的样式 


其中，每个组件中必须包含 template 模板结构，而 script 行为和 style 样式是可选的组成部分。



vue 规定：**.vue 组件中的 data 必须是一个函数**，不能直接指向一个数据对象。

```js
data(){
	return {
		username:"lsj"
	}
}
```



让style支持less只需要添加 lang="less" 属性即可，为了防止组件之间的样式冲突，只需要加 **scoped** 属性即可

```js
<style lang="less" scoped>
</style>
```



#### 使用组件的三个步骤

1. 使用 import 引入组件
2. 使用 compons 节点注册组件
3. 在 template 中以标签形式使用组件



**通过 Vue.component() 方法，可以注册全局组件。**



#### 自定义属性props

```js
props: {
  name: {
    type: String, // 值类型
    default: '', // 默认值
    required: true // 必填项
  }
}
```



### 生命周期

常用：

created 创建后

> 此时组件的props/data/methos已创建好，都可用。但是组件的模板结构尚未完成。（此时是发起 Ajax 最早的时机，请求数据）

mounted 渲染后

> 此时已经将内存的HTML结构渲染到浏览器之中，此时可以操作DOM（此时是操作dom最早的时机）

updated 更新

> 能够操作到最新的 DOM 元素

destroyed 销毁

<img src="https://cdn.leonus.cn/img/imglifecycle.webp" alt="" style="width:400px;height:auto;">



### 组件之间数据共享

#### 父向子传数据

通过自定义属性即可



#### 子向父传数据

通过自定义事件

**子组件代码如下：**

```js
<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    add() {
      this.count += 1;
      // 通过$emit定义numchange事件，并进行传值。
      //执行add函数时numchange事件被触发，然后父组件执行getNewCount函数
      //getNewCount函数的参数就是$emit传的值，即this.count
      this.$emit('numchange', this.count)
    }
  }
}
</script>
```

**父组件代码如下：**

```js
<template>
  <Son @numchange="getNewCount"></Son>
</template>

<script>
export default {
  data() {
    return {
      countFromSon: 0
    }
  },
  methods: {
    getNewCount(val) {
      this.countFromSon = val
    }
  }
}
</script>
```

#### 兄弟之间的数据共享

 vue2.x 中，兄弟（爷孙等也可以）组件之间数据共享的方案是 EventBus。

- 创建 eventBus.js 模块，并向外共享一个 Vue 的实例对象 
- 在数据发送方，调用 bus.$emit('事件名称', 要发送的数据) 方法触发自定义事件 
- 在数据接收方，调用 bus.$on('事件名称', 事件处理函数) 方法注册一个自定义事件

<img src="https://cdn.leonus.cn/img/img2022-03-12__16.18.webp" alt="" style="width:400px;height:auto;">


### ref引用

ref 用来辅助开发者在不依赖于 jQuery 的情况下，获取 DOM 元素或组件的引用。 

每个 vue 的组件实例上，都包含一个 $refs 对象，里面存储着对应的 DOM 元素或组件的引用。默认情况下， 组件的 $refs 指向一个空对象。

#### 使用 ref 引用 DOM 元素

```js
<template>
  <div>
    <h3 ref="demoref">ref测试</h3>
    <button @click="setref">点我</button>
  </div>
</template>

<script>
export default {
  methods: {
    setref() {
      this.$refs.demoref.style.backgroundColor = 'red'
    }
  }

}
</script>
```

#### 使用 ref 引用组件

```js
<template>
  <div>
    <Mycount ref="countref"></Mycount>
    <button @click="getref">点我</button>
  </div>
</template>

<script>
import Mycount from "@/components/mycount.vue";



export default {
  namme: 'App',
  components: {
    Mycount
  },
  methods: {
    getref() {
      // 通过ref调用组件的方法
      this.$refs.countref.add()
    }
  }
}
</script>
```

#### this.$nextTick(cb) 方法 

**组件的 `$nextTick(cb)` 方法，会把 cb 回调推迟到下一个 DOM 更新周期之后执行。**

通俗的理解是：等组件的 DOM 更新完成之后，再执行 cb 回调函数。从而能保证 cb 回调函数可以操作到最新的 DOM 元素。



### 动态组件

`<component>` 组件，专门用来实现动态组件的渲染。

```js
<component :is="comName"></component>
```



默认情况下，切换动态组件时无法保持组件的状态。此时可以使用 vue 内置的 `<keep-alive>` 组件保持动态组件的状态。

```js
<keep-alive>
	 <component :is="comName"></component>
</keep-alive>
```

**keep-alive 对应的生命周期函数** 

- 当组件被缓存时，会自动触发组件的 deactivated 生命周期函数。 
- 当组件被激活时，会自动触发组件的 activated 生命周期函数。

keep-alive 的 include 属性用来指定：只有名称匹配的组件会被缓存。多个组件名之间使用英文的逗号分隔。

```js
<keep-alive include="Left, Right">
	 <component :is="comName"></component>
</keep-alive>
```



### 插槽

插槽（Slot）是 vue 为组件的封装者提供的能力。

允许开发者在封装组件时，把不确定的、希望由用户指定的部分定义为插槽。

可以把插槽认为是组件封装期间，为用户预留的内容的占位符。

在封装组件时，可以通过 `<slot>` 元素定义插槽，从而为用户预留内容占位符。

封装组件时，可以为预留的插槽提供**后备内容（默认内容）**。如果组件的使用者没有为插槽提供任何内容，则后备内容会生效。

如果在封装组件时需要预留多个插槽节点，则需要为每个  插槽指定具体的 name 名称。这种带有具体 名称的插槽叫做“具名插槽”。

```js
<slot name="demo">这里是后备内容</slot>
```

在向具名插槽提供内容的时候，我们可以在一个 `<template>` 元素上使用 `v-slot` 指令，并以 v-slot 的参数的形式提供其名称。

跟 v-on 和 v-bind 一样，v-slot 也有缩写，即把参数之前的所有内容 (v-slot:) 替换为字符 `#`。例如 v-slot:header 可以被重写为 #header

App.vue：

```js
<Mycount>
  <template v-slot:s1>aaaaaaaaaaaa</template>
  <template #s2>bbbbbbbbbbbbb</template>
  <template #s3>cccccccccccccc</template>
</Mycount>
```

组件：

```js
<p>
  <slot name="s1"></slot>
</p>
<p>
  <slot name="s2"></slot>
</p>
<p>
  <slot name="s3"></slot>
</p>
```



#### 作用域插槽

在封装组件的过程中，可以为预留的插槽绑定 props 数据，这种带有 props 数据的  叫做“作用 域插槽”

组件中

```js
<!-- 在封装组件时，为预留的 <slot> 提供属性对应的值，这种用法，叫做 “作用域插槽” -->
<slot name="content" msg="hello vue.js" :user="userinfo"></slot>
```

App.vue

```js
<Mycount>
  <template #content="obj"> // obj是一个对象，建议写成scope
    {{ obj.msg }} // hello vue.js
  </template>
</Mycount>
```

**作用域插槽对外提供的数据对象，可以使用解构赋值简化数据的接收过程。**

```js
<Mycount>
  <template #content="{ msg }"> 
    {{ msg }} // 效果同上
  </template>
</Mycount>
```



### 自定义指令

在每个 vue 组件中，可以在 `directives` 节点下声明私有自定义指令。

**定义**

```js
<script>
export default {
  namme: 'App',
  directives: {
    color: {
      bind(el) {
        el.style.color = 'red'
      }
    }
  }
}
</script>
```

**使用**

使用只需要在自定义指令前加上 v-

```js
<p v-color>1111111111111111</p>
```

#### 动态绑定参数

在 template 结构中使用自定义指令时，可以通过等号（=）的方式，为当前指令动态绑定参数值

在声明自定义指令时，可以通过形参中的第二个参数，来接收指令的参数值

```js
<template>
  <div>
    <p v-color="color">1111111111111111</p> // 不能直接输入值
  </div>
</template>

<script>

export default {
  namme: 'App',
  data() {
    return {
      color: 'blue'
    }
  },
  directives: {
    color: {
      bind(el, binding) { // binding是一个对象
        el.style.color = binding.value //通过.value可以获取到动态参数的值
      }
    }
  }
}
</script>
```

bind 函数只调用 1 次：当指令第一次绑定到元素时调用，当 DOM 更新时 bind 函数不会被触发。 update 函 数会在每次 DOM 更新时被调用。

如果 bind 和update 函数中的逻辑完全相同，则对象格式的自定义指令可以简写成函数格式

```js
<template>
  <div>
    <p v-color="color">1111111111111111</p>
    <button @click="color='red'">点我切换成红色</button>
  </div>
</template>

<script>

export default {
  namme: 'App',
  data() {
    return {
      color: 'blue'
    }
  },
  directives: {
    // color: {
    //   bind(el, binding) {
    //     el.style.color = binding.value
    //   },
    //   update(el, binding) {
    //     el.style.color = binding.value
    //   }
    // }
    // 简写形式
    color(el, binding) { 
      el.style.color = binding.value
    }
  }
}
</script>
```

全局共享的自定义指令需要通过 `Vue.directive()` 进行声明

main.js

```js
Vue.directive('color', (el, binding) => {
    el.style.color = binding.value
})
```



### 路由

就是对应关系

#### SPA与路由

SPA 指的是一个 web 网站只有唯一的一个 HTML 页面，所有组件的展示与切换都在这唯一的一个页面内完成。 

此时，不同组件之间的切换需要通过前端路由来实现。

结论：在 SPA 项目中，不同功能之间的切换，要依赖于前端路由来完成！

#### 什么是前端路由

通俗易懂的概念：Hash 地址与组件之间的对应关系。

#### 路由的工作方式

+ 用户点击了页面上的路由链接 
+ 导致了 URL 地址栏中的 Hash 值发生了变化 
+ 前端路由监听了到 Hash 地址的变化 
+ 前端路由把当前 Hash 地址对应的组件渲染都浏览器中

#### vue-router

vue-router 是 vue.js 官方给出的路由解决方案。它只能结合 vue 项目进行使用，能够轻松的管理 SPA 项目 中组件的切换。 

vue-router 的官方文档地址：https://router.vuejs.org/zh/

**vue-router使用教程**

- 安装 vue-router 包 
- 创建路由模块 
- 导入并挂载路由模块 
- 声明路由链接和占位符

##### 安装vue-router

**npm i vue-router@3.5.2**

##### 创建路由模块

在 src 源代码目录下，新建 router/index.js 路由模块，并初始化如下的代码

```js
import Vue from "vue";
import VueRouter from "vue-router";

Vue.use(VueRouter)

const router = new VueRouter()

export default router
```

##### 导入并挂载

在 src/main.js 入口文件中，导入并挂载路由模块

```js
import Vue from 'vue'
import App from './App.vue'
import router from "@/router/";  // 导入

Vue.config.productionTip = false
Vue.directive('color', (el, binding) => {
    el.style.color = binding.value
})

new Vue({
    render: h => h(App),
    router // 挂载
}, ).$mount('#app')
```

##### 声明路由链接和占位符

在 src/App.vue 组件中，使用 vue-router 提供的 `<router-link>` 和 `<router-view>` 声明路由链接和占位符

```js
<template>
  <div>
    <router-link to="/home">首页</router-link>
    <router-link to="/movie">电影</router-link>
    <router-link to="/about">关于</router-link>

    <router-view></router-view>
  </div>

</template>
```

##### 声明路由的匹配规则

在 src/router/index.js 路由模块中，通过 routes 数组声明路由的匹配规则

```js
import Vue from "vue";
import VueRouter from "vue-router";

import Home from "@/views/Home.vue";
import Movie from "@/views/Movie.vue";
import About from "@/views/About.vue"; // 导入组件

Vue.use(VueRouter)

const routes = [ // 定义路由规则列表
    { path: '/home', component: Home },
    { path: '/movie', component: Movie },
    { path: '/about', component: About }
]


const router = new VueRouter({ routes }) 

export default router
```

##### 路由重定向

路由重定向指的是：用户在访问地址 A 的时候，强制用户跳转到地址 C ，从而展示特定的组件页面。 通过路由规则的 `redirect` 属性，指定一个新的路由地址，可以很方便地设置路由的重定向

```js
{ path: '/', redirect: '/home' }
```

##### 嵌套路由

**声明子路由链接和子路由占位符**

在 About.vue 组件中，声明 tab1 和 tab2 的子路由链接以及子路由占位符。

```js
<template>
  <div>
    <p>关于插件</p>
    <router-link to="/about/t1">tab1</router-link>
    <router-link to="/about/t2">tab2</router-link>

    <router-view></router-view>
  </div>
</template>
```

在 src/router/index.js 路由模块中，导入需要的组件，并使用 children 属性声明子路由规则

```js
import Vue from "vue";
import VueRouter from "vue-router";

import Home from "@/views/Home.vue";
import Movie from "@/views/Movie.vue";
import About from "@/views/About.vue";
import Tab1 from "@/views/Tab1.vue";
import Tab2 from "@/views/Tab2.vue"; // 导入子组件

Vue.use(VueRouter)

const routes = [
    { path: '/home', component: Home },
    { path: '/movie', component: Movie },
    {
        path: '/about',
        component: About,
        children: [
            { path: 't1', component: Tab1 }, // 声明子路由规则
            { path: 't2', component: Tab2 }
        ]
    }
]
```



##### 动态分配路由

动态路由指的是：把 Hash 地址中可变的部分定义为参数项，从而提高路由规则的复用性。 在 vue-router 中使用英文的冒号（:）来定义路由的参数项。

```js
{ path: '/home/:id', component: Home }
```

在动态路由渲染出来的组件中，可以使用 `this.$route.params` 对象访问到动态匹配的参数值。

app.vue

```js
<router-link to="/movie/1">电影1</router-link>
<router-link to="/movie/2">电影2</router-link>
<router-link to="/movie/3">电影3</router-link>
<router-link to="/movie/4">电影4</router-link>
```

index.js

```js
{ path: '/movie/:id', component: Movie }
```

movie.vue

```js
<template>
  <div>
    <p>电影插件 -- {{ this.$route.params.id }}</p>
  </div>
</template>

<script>
export default {

}
</script>
```

为了简化路由参数的获取形式，vue-router 允许在路由规则中开启 props 传参。

index.js

```js
{ path: '/movie/:id', component: Movie, props: true }
```

movie.vue

```js
<template>
  <div>
    <p>电影插件 -- {{ id }}</p>
  </div>
</template>

<script>
export default {
  props: ['id']
}
</script>

<style>
</style>
```

##### 编程导航API

1. this.$router.**push**('hash 地址') 

	- 跳转到指定 hash 地址，并增加一条历史记录 

2. this.$router.**replace**('hash 地址') 
	- 跳转到指定的 hash 地址，并替换掉当前的历史记录 
3. this.$router.**go**(数值 n) 
	- 实现导航历史前进、后退

##### 导航守卫

导航守卫可以控制路由的访问权限。

每次发生路由的导航跳转时，都会触发全局前置守卫。因此，在全局前置守卫中，程序员可以对每个路由进行访问权限的控制。

```js
// 调用路由实例对象的 beforeEach 方法，即可声明 “全局前置守卫”
// 每次发生路由跳转的时候，都会自动触发 fn 这个 “回调函数”
router.beforeEach(fn) // 写在实例后面
```

全局前置守卫的回调函数中接收 3 个形参

```js
router.beforeEach((to, from, next) => {
    // to 是即将访问的路由的信息对象
    // from 是将要离开的路由的信息对象
    // next 是一个函数，调用next()表示放行，允许这次路由导航
    // 没有权限强行跳转到登陆界面 next('/login')，或者不允许跳转next(false)
    
    // 例子
    if (to.path == '/admin') {
        const token = localStorage.getItem('token')
        if (token) {
            next()
        } else {
            next('/login')
        }

    } else {
        next()
    }
});
```





## 其他

### 常用命令

```bash
npm init –y 
npm i xxx  == npm install xxx
npm run xxx
```



### 知识补充

vue-devtools 浏览器调试vue插件
