# Vue

Vue.js 的核心是一个采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

## 如何使用Vue?

1. 通过导入本地vue.js文件

2. 导入cdn的外部vue.js文件

   ```html
   <!-- 开发环境版本，包含了有帮助的命令行警告 -->
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   或
   <!-- 生产环境版本，优化了尺寸和速度 -->
   <script src="https://cdn.jsdelivr.net/npm/vue"></script>
   ```



## Vue基本功能与组件

### 声明式渲染

```html
<div id="app">
  {{ message }}
    <!--通过下方vue中类似于键值对格式中的key值获取数据
		这个数据和DOM进行关联,成为响应式的(修改message的值后html上的值也会立即发生改变)
-->
</div>
```

```js
var app = new Vue({
  el: '#app',
    //el是一个选择器,选择到dom对象,在这里用的是id选择器选择app
    //不建议直接选择body与html
  data: {
    message: 'Hello Vue!'
  }
})
```

Vue不再和 HTML 直接交互了。一个 Vue 应用会将其挂载到一个 DOM 元素上 (如上方的例子是#app) 然后对其进行完全控制。那个 HTML 是我们的入口，但其余都会发生在新创建的 Vue 实例内部。



除了文本插值，我们还可以像这样来绑定元素 attribute：

```html
<div id="app-2">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>
```

```js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '页面加载于 ' + new Date().toLocaleString()
  }
})
```

spand标签中的`v-bind` attribute 被称为**指令**。指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊 attribute。它们会在渲染的 DOM 上应用特殊的响应式行为。在这里，该指令的意思是：“将这个元素节点的 `title` attribute 和 Vue 实例的 `message` property 保持一致”。



### 指令

Vue中的指令都以"v-"开头的特殊HTML元素属性,属性的值是JavaScript表达式

当表达式的值发生改变的时候,将其产生的影响渲染到dom中

1. v-text与v-html

   语法:

   ​	v-text='表达式'

   ​	v-html='表达式'

   作用:将Model中的数据绑定到view中

   两个都从model单向绑定到html中。其中text把字符当成文本渲染到页面中，html会将字符文本中的html元素解析为html渲染到页面中

2. v-bind

   语法：

   ​	v-bind：‘属性’=‘表达式’

   或是缩写 “：”号

   作用：将数据绑定到DOM元素的属性上或绑定样式

   ​			

3. v-once

   语法：v-once：属性=‘表达式’

   作用：单向的数据绑定，数据只绑定一次，Model中的数据发生改变不会影响view

   


### 判断条件与循环

可以通过vue的判断操作来控制某些标签是否需要显示在页面中，具体操作如下：

```html
<<div id="app-3">
	<p v-if="seen==='A'">结果为{{seen}}显示数据1在页面中</p>
	<p v-else-if="seen==='B'">结果为{{seen}}显示数据2在页面中</p>
	<p v-else>结果为C</p>
<!--三个=号表示全等于
	两个=号判断类型
-->
</div>
```

```js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: A
  }
})

//输出结果为:结果为A显示数据1在页面中
```

对于多条数据,也可以通过`v-for` 指令进行显示

```html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
        <!--类似于java中的foreach循环-->
      {{ todo.text }}
    </li>
  </ol>
</div>
```

```js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```

在控制台里，输入 `app4.todos.push({ text: '新项目' })`，可以手动给列表最后添加一行数据；

unshfit：在数据最前面插入数据

v-for指令在更新数据时采用'**就近原则**',不会从重新排列位置,当顺序发生改变时,dom不会改变dom元素

### 处理用户输入

为了让用户和你的应用进行交互，我们可以用 `v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：

```html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">反转消息</button>
    <!--Vue通过v-on绑定事件-->
    <!--或者缩写为@click-->
    <!--v-on:click表示这是一个点击事件-->
</div>
```

```js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
        //点击按钮对字符串进行反转
    }
  }
})
//reverseMessage为方法名,由自己随意定义
```

上面的方法更新了页面的内容，但没有触碰 DOM——所有的 DOM 操作都由 Vue 来处理，编写的代码只需要关注逻辑层面即可。



Vue 还提供了 `v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定。它本质上不过是一个语法糖,主要负责监听用户的输入事件以及更新数据,并对一些极端场景进行特殊处理

```html
<div id="app-6">
  <p>{{ message }}</p>
    <!--双向绑定的v-model会忽略表单中的value属性-->
    <!--也会忽略多选框与单选框中的check属性-->
    <!--如果要获取单选框或复选框中的val值,Vue中的数据类型应该是数组-->
  <input v-model="message">
</div>

<!--v-model使用在下拉框中会忽略selected属性-->
```

```js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})

//当input框中的数据更改时,vue数据也会跟着改变,同理vue的数据改变后input框的数据也会改变
```

v-model只能在表单中使用



v-model的修饰符

1. .lazy  -> 延时加载,(例如:文本框在输入内容后不会立即绑定到vue的数据中,只有当文本框失去焦点时,数据才绑定)

```html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model.lazy="message">
</div>
```

2. .number -> 将输入的数字转换为number类型,如果不能转换,它返回原始数据

   ```html
   <div id="app-6">
     <p>{{ message }}</p>
     <input v-model.number="message">
   </div>
   <!--采用的是从左到右逐位转换-->
   ```

3. .trim ->去除输入信息的前后空格



### 组件

组件是为了拆分Vue实例的代码块,能以不同的组件来拆分不同的功能模块

组件又分为:

- 全局组件
  - 所有的Vue实例都可以使用
- 私有组件
  - 在Vue实例中定义的组件,只能在定义的Vue实例中使用
- Vue实例也是一个组件

```html
<ol>
  <!-- 创建一个 todo-item 组件的实例
	   它能将我们定义的组件内容放到html页面中

		在使用组件的时候,不能直接使用驼峰作为标签名
		可以用-表示后一个字母为大写,代替驼峰
-->
  <todo-item></todo-item>
</ol>
```

```js
// 定义名为 todo-item 的新组件
//定义组件的dom元素有且只能有一个根元素
//组件的名称要么全小写,要么采用驼峰命名法
Vue.component('todo-item', {
  template: '<li>这是个全局组件</li>'
})

var app = new Vue(...)
```

但是上方的组件文本已经被固定，在正常情况下并不好用。我们需要在外界动态的加载数据进入组件，实现动态功能

```html
<div id="app-7">
  <ol>
    <!--
      现在我们为每个 todo-item 提供 todo 对象
      todo 对象是变量，即其内容可以是动态的。
      我们也需要为每个组件提供一个“key”，稍后再
      作详细解释。
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```

```js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: '蔬菜' },
      { id: 1, text: '奶酪' },
      { id: 2, text: '随便其它什么人吃的东西' }
    ]
  }
})
```

Vue属性绑定,文本使用{{}},属性使用v-bind

### Axios

支持node端和浏览器端的http库，在node.js中可以发送http请求，在游览器中可以发送ajax请求

1. 安装

```html
<div id="vue">
			<div>{{info.name}}</div>
</div>
```

```js
<script type="text/javascript">
			
			var vm = new Vue({
				el:'#vue',
				
				data(){
					return{
						info:null
                        //将info设置为null,它会自动注入所有参数
					}
				},
				
				mounted(){		//钩子函数
					axios.get('data.json').then(response=>(this.info=response.data));
                    //data.json外部的json文件
                    //用axios获取外部的json文件,然后将json数据添加倒info参数中
				}
                
			});
			
</script>
```

### 计算属性

先看一个简单例子

```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```

```js
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})


//输出结果
//Original message: "Hello"
//Computed reversed message: "olleH"
```

计算属性和方法的主要区别在于:

**计算属性是基于它们的响应式依赖进行缓存的**。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。相比于方法,我们每次使用它,它都会再次执行一遍。

如果我们要对一个数据量十分庞大的json进行多次数据访问。使用方法会占用大量的性能开销，而使用计算属性我们在参数未发生改变的情况下，再次访问会直接在缓存当中进行读取，节约性能。

### 插槽

首先来段示例

```html
<div id="vue">
    <!--第四步:绑定slot插槽并提供数据-->
    <!--通过todo这个组件名,获取到我们声明的slot插槽组件-->
    <todo>
        <!--然后我们对插槽组件中的两个slot进行插入-->
        <!--
			todo-heads:表示我们声明的组件标签
			slot="todo-heads":表示我们对插槽中name值为todo-heads的标签进行替换
			:heads: 其中":"符号为v-bind的缩写,heads为我们需要传入的参数名,="heads"表示传入的参数
		-->
        <todo-heads slot="todo-heads" :heads="heads"></todo-heads>
        <!--传入集合我们需要循环把它的所有数据拿出来
			v-for="item in content":其中content为集合名 in固定写法,item是我们自己声明的参数,用于拿取数据
			最后通过:content将数据传入
		-->
        <todo-content slot="todo-content" v-for="item in content" :content="item"></todo-content>
    </todo>
</div>
```

```js
//slot:插槽

//第一步:我们定义一个插槽
//Vue.component({})定义一个组件,todo:组件名
Vue.component("todo",{
    // "\"这个字符代表换行
	template:'<div>\
				<slot name="todo-heads"></slot>\
				<ul>\
					<slot name="todo-content"></slot>\
				</ul>\
			</div>'
});

//第二步:给插槽定义需要的标签
//我们需要动态数据的标签
//通过props:['属性名']从外界获取数据
Vue.component("todo-heads",{
	props:['heads'],
	template:'<div>{{heads}}</div>'
});
Vue.component("todo-content",{
	props:['content'],
	template:'<li>{{content}}</li>'
});

//第三步:声明测试数据
var vm = new Vue({
	el:'#vue',
	data:{
		heads:"图书列表",
		content:['JAVA','C#','C++','WEB']	//它是一个集合
	}

});
```

### 自定义事件内容分发

```html
		<div id="vue">
			<todo>
				<todo-heads slot="todo-heads" :heads="heads"></todo-heads>
				<todo-content slot="todo-content" v-for="(item,index) in content" :content="item" :index="index"  @remove="removeItems()" :key="index"></todo-content>
                <!--第二步,在html视图中获取到Vue中的方法
					通过v-on或是缩写@绑定方法
					拿到组件中的remove方法,再将vue实例中的方法给它进行绑定
				-->
			</todo>
		</div>
```

```js
//slot:插槽
Vue.component("todo",{
	template:'<div>\
				<slot name="todo-heads"></slot>\
				<ul>\
					<slot name="todo-content"></slot>\
				</ul>\
			</div>'
});

Vue.component("todo-heads",{
	props:['heads'],
	template:'<div>{{heads}}</div>'
});
Vue.component("todo-content",{
	props:['content','index'],
	template:'<li>{{index}}--------{{content}} <button @click="remove" >删除</button></li>',
	methods:{
        //第三步,组件去调用绑定的方法运行
		remove: function (){
			this.$emit('remove',this.index);
            //这里获取index有两种方式:
            	//1.通过方法传参获取
           		//2.直接this拿取
		}
	}
});

var vm = new Vue({
	el:'#vue',
	data:{
		heads:"图书列表",
		content:['JAVA','C#','C++','WEB']
	},
    
    //自定义事件第一步
    //在Vue实例中声明一个方法
	methods:{
		removeItems:function(index){
			console.log("删除了"+this.content[index]+"OK");
			this.content.splice(index,1);		//删除集合从指定下标开始的数量
		}
	}
});
```

正常情况下,组件是无法调用到vue实例中的方法的，且组件也无法对组件之外的元素进行修改。所以我们使用视图层html当一个中转站。在html中获取Vue实例中的方法，再将这个方法绑定到组件中，我们就可以通过组件使用到这个方法



### vue-cli程序

1.从Node官网下载安装Node.js

2.安装Node.js的镜像加速器cnpm

​		管理员启动cmd执行语句 npm install -g cnpm --registry=https://registry.npm.taobao.org

​		然后更改默认使用淘宝镜像:npm config set registry https://registry.npm.taobao.org

3.安装vue-cli

​		管理员启动cmd执行语句 cnpm install vue-cli -g

​		安装完成之后执行vue list测试是否成功,并查看可以基于哪些模板创建vue应用

4.创建一个Vue项目

​	随便创建一个存放项目的文件夹在电脑中

​	cmd访问路径到项目地址,执行: vue init webpack myvue

//webpack:使用webpack创建项目

//myvue:项目名,自己随意创建

5.启动项目

​	创建完成之后,在cmd访问到项目路径,运行:npm run dev即可启动项目

​	按下ctrl+c即可停止项目

​	或是在idea中的Terminal中输入npm run dev运行  (在idea中运行需要以管理员身份运行idea)

​	//tips:配置端口号在config目录下的index.js文件 





## Vue的生命周期

![1469407-20190428112508081-220966019](\assets\1469407-20190428112508081-220966019.png)

## Vue钩子

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="./lib/vue-2.4.0.js"></script>
</head>

<body>
  <div id="app">
    <input type="button" value="修改msg" @click="msg='No'">
    <h3 id="h3">{{ msg }}</h3>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        msg: 'ok'
      },
      methods: {
        show() {
          console.log('执行了show方法')
        }
      },
      beforeCreate() { // 这是我们遇到的第一个生命周期函数，表示实例完全被创建出来之前，会执行它
        // console.log(this.msg)
        // this.show()
        // 注意： 在 beforeCreate 生命周期函数执行的时候，data 和 methods 中的 数据都还没有没初始化
      },
      created() { // 这是遇到的第二个生命周期函数
        // console.log(this.msg)
        // this.show()
        //  在 created 中，data 和 methods 都已经被初始化好了！
        // 如果要调用 methods 中的方法，或者操作 data 中的数据，最早，只能在 created 中操作
      },
      beforeMount() { // 这是遇到的第3个生命周期函数，表示 模板已经在内存中编辑完成了，但是尚未把 模板渲染到 页面中
        // console.log(document.getElementById('h3').innerText)
        // 在 beforeMount 执行的时候，页面中的元素，还没有被真正替换过来，只是之前写的一些模板字符串
      },
      mounted() { // 这是遇到的第4个生命周期函数，表示，内存中的模板，已经真实的挂载到了页面中，用户已经可以看到渲染好的页面了
        // console.log(document.getElementById('h3').innerText)
        // 注意： mounted 是 实例创建期间的最后一个生命周期函数，当执行完 mounted 就表示，实例已经被完全创建好了，此时，如果没有其它操作的话，这个实例，就静静的 躺在我们的内存中，一动不动
      },


      // 接下来的是运行中的两个事件
      beforeUpdate() { // 这时候，表示 我们的界面还没有被更新【数据被更新了吗？  数据肯定被更新了】
        /* console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
        console.log('data 中的 msg 数据是：' + this.msg) */
        // 得出结论： 当执行 beforeUpdate 的时候，页面中的显示的数据，还是旧的，此时 data 数据是最新的，页面尚未和 最新的数据保持同步
      },
      updated() {
        console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
        console.log('data 中的 msg 数据是：' + this.msg)
        // updated 事件执行的时候，页面和 data 数据已经保持同步了，都是最新的
      }
    });
  </script>
</body>

</html>
```





## Vue-Cli

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统，它能将各种vue工具进行平稳衔接

#### 使用Vue-CLI创建单页面应用程序



## Webpack

webpack安装

cmd管理员模式运行:npm install webpack -g

与:npm install webpack-cli -g

安装完后执行:webpack -v查看是否安装成功与安装版本



## vue-router

在当前项目路径下执行: npm in  tall vue-router --save-dev	导入router的包

然后在src路径下的main.js文件中导入router  语法:import VueRouter from 'vue-router'

添加vue的显示声明使用

```vue
//显示声明使用VueRouter
Vue.use(VueRouter)
```

随后在src创建router文件夹,配置router的主配置,主要负责分配路由路径

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
//导入vue与router

import Content from '../components/Content'
import Main from '../components/Main'
//导入需要的外部组件


//安装路由
Vue.use(VueRouter)


//配置导出路由
export  default  new VueRouter({
  routes: [
    {
      //路由的路径
      path: '/content',
      name: 'content',
      //跳转的组件
      component: Content
    },
    {
      //路由的路径
      path: '/main',
      name: 'main',
      //跳转的组件
      component: Main
    }
  ]
});

```

随后需要在main.js中导入路由文件,只需要告诉系统文件在哪个路径下

```js
import router from './router'  //自动扫描里面的路由配置

new Vue({
  el: '#app',
  //配置路由
  router,
  components: { App },
  template: '<App/>'
})
```

然后就可以在页面中使用

```vue
	<router-link to="/main">首页</router-link>
    <router-link to="/content">内容页</router-link>
	//表示为html中的<a></a>标签

	//显示路由视图
    <router-view></router-view>
```

### 路由嵌套

如果全是用一级路由时，路由管理就变得很臃肿，有点乱，路由有父子关系的话，嵌套路由会更好。嵌套也就是路由中的路由的意思，组件中可以有自己的路由导航和路由容器（router-link、router-view），通过配置children可实现多层嵌套，在vue组件中使用<router-view>就可以了。

#### 嵌套路由的使用场景：

应用最多的就是选项卡，在选项卡中，顶部有多个导航栏，中间的主体显示的是内容；这个时候，整个页面是一个路由，然后点击选项卡切换不同的路由来展示不同的内容，就是中间的主体显示的是内容就是页面路由下的子路由，这就是路由中嵌套路由。

```js
import UserList from '../components/user/List'
import UserProfile from '../components/user/Profile'
//导入子组件路径

//将子路由嵌套在路由路径中
{
      //路由的路径
      path: '/main',
      name: 'main',
      //跳转的组件
      component: Main,
      //嵌套路由
          children:[
        {
          path:'/user/Profile',
          component: UserProfile
        },
        {
          path:'/user/List',
          component: UserList
        }
      ]


    }
```

```vue
//通过router-link引用
<router-link to="/user/profile">个人信息</router-link>

//通过router-view引入子路由视图
<router-view/>
```





## vue+elementUI

创建vue项目+elementui依赖流程

首先创建一个vue项目 vue init webpack vue-elementui

```cmd
# 进入项目目录
cd vue-elementui
# 安装 vue-router
npm install vue-router --save-dev
# 安装 element-ui
npm i element-ui -s
# 安装依赖
npm install
# 安装sass加载器
npm install sass-loader node-sass --save-dev
# 启动测试
npm run dev


# 当npm出错时可以更改为cnpm
```

## 参数传递与重定项

传递参数主要分为两大类

- ##### 编程式的导航 router.push

编程式导航传递参数有两种类型：字符串、对象。

### 字符串

字符串的方式是直接将路由地址以字符串的方式来跳转，这种方式很简单但是不能传递参数：

```javascript
this.$router.push("home");
```

### 对象

想要传递参数主要就是以对象的方式来写，分为两种方式：命名路由、查询参数，下面分别说明两种方式的用法和注意事项。

#### 命名路由

命名路由就是在注册路由的时候声明了name属性的路由

命名路由传递参数需要使用params来传递，这里一定要注意使用params不是query。目标 页面接收传递参数时使用params

 **特别注意：命名路由这种方式传递的参数，如果在目标页面刷新是会出错的**。数据丢失

代码如下：

```vue

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button @click="routerTo">click here to news page</button>
  </div>
</template>
 
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods:{
    routerTo(){
      this.$router.push({ name: 'news', params: { userId: 123 }});
    }
  }
}
</script>
```

接受传递的参数：

```vue
<template>
  <div>
    this is the news page.the transform param is {{this.$route.params.userId}}
  </div>
</template>
<script>
  
</script>
```

#### 查询参数

查询参数其实就是在路由地址后面带上参数和传统的url参数一致的，传递参数使用query而且必须配合path来传递参数而不能用name，目标页面接收传递的参数使用query。
注意：和name配对的是params，和path配对的是query
使用方法如下：

```vue
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button @click="routerTo">click here to news page</button>
  </div>
</template>
 
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods:{
    routerTo(){
      this.$router.push({ path: '/news', query: { userId: 123 }});
    }
  }
}
</script>
 
<style>
</style>
```

接收:

```vue
<template>
  <div>
    this is the news page.the transform param is {{this.$route.query.userId}}
  </div>
</template>
<script>
</script>
```



- ##### 声明式的导航<router-link>

```vue
1.前端传递参数
:to="{name:'/user/profile',params:{id:1}}"
//传递参数,  name:为访问路径, params:为要传递的参数,id为参数名

2.在路由配置中接收参数
path: 'user/profile/:id/:参数2'
component: UserProfile,
props: true
//设置props为ture,可以在组件中直接通过props[]获取值

3.组件展示参数
{{$route.params.id}}

tips:
可以在路由配置中设置props:true
就可以在组件中直接通过props:[id]拿取参数
```

#### 重定项

```js
//在路由设置中编写
routes: [{
    path: '/jump',
    redirect:'/main'
}]
//即可通过/jump路径重定项到路径为main的页面
```

## 页面404导航

创建一个404访问后的专用页面,随后在路由里面配置

```js
{
    //路径设置path后,路由会判断,所有设置中是否有能匹配到的路径,如果没有则访问路径*
    path: '*',
    component: NotFound
}
```

## 路由钩子

beforeRouteEnter:

//进入路由前执行的钩子

```vue
//一般被当成过滤器进行过滤操作
beforeRouteEnter:(to,from,next)=>{
	//进入钩子之后,程序会停在钩子
	next();
	//只有当执行到next()之后才会跳出钩子执行后面的操作
	//所以一般情况下,所有的钩子函数都需要加next()
}
```

boforeRouteLeave:

//进入路由后执行的钩子

```vue
//一般被当成过滤器进行过滤操作
boforeRouteLeave:(to,from,next)=>{
	next();
}
```

//钩子的语法