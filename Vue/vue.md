# vue
***
# 1.	vue指令大全
带有前缀v-的称为vue的指令
###### （1）v-text
用来更新textContent,等同于JS的text属性。例如`<p v-text=’msg’></p>`等价于`<p>{{msg}}</p>`
###### （2）v-html
输出html，等同于js的innerHtml属性
###### （3）v-pre
v-pre主要用于跳过这个元素和它的子元素编译过程，可以用来显示原始的Mustache标签。跳过大量没有指令的节点加快编译。
###### （4）v-cloak
当网络较慢，网页还在加载 Vue.js ，而导致 Vue 来不及渲染，这时页面就会显示出 Vue 源代码。我们可以使用 v-cloak 指令来解决这一问题。解决屏幕闪动的问题。用来保持在元素上直到关联实例结束时进行编译。
###### （5）v-once
v-once关联的实例，只会渲染一次。之后的重新渲染，实例及其所有的子节点将被视为静态内容跳过，可以用于优化更新性能。
###### （6）v-if
实现条件渲染，会根据表达式值的真假条件来渲染元素。
###### （7）v-else
v-else是搭配v-if使用的，它必须紧跟在v-if或者v-else-if后面，否则不起作用。当v-if不满足时，显示v-else的内容。
###### （8）v-else-if
v-else-if充当v-if的else-if块，可以链式的使用多次，可以更加方便的实现switch语句。
###### （9）v-show
也是根据条件展示元素，和v-if不同的是，如果v-if的值为false，则这个元素被销毁，不在dom中。但是v-show的元素会始终被渲染并保存在dom中，它只是简单的切换css的display属性为none。
注意：v-if有更高的切换开销，v-show有更高的初始渲染开销。如果需要频繁切换，则优先使用v-show，如果初始条件不太可能改变，则用v-if更好。
###### （10）v-for
遍历数组来进行渲染，有下面两种遍历形式
使用for...in :`<div v-for="(item,index) in items"></div>`  //index是一个可选参数，表示当前项的索引;
使用for...of : `<div v-for=”item of items”></div>`
为保证对象唯一性，可用:key="item.id"来绑定，key绑定的值可以是number/string
在v-for中，拥有对父作用域属性的完全访问权限
注意：当v-for和v-if同处于一个节点时，v-for的优先级比v-if更高。这意味着v-if将运行在每个v-for循环中。
###### （11）v-bind
用于动态的绑定一个或多个特性，可简写为一个冒号 :name等价于v-bind:name
1.	属性绑定
v-bind:name=”name”  //引号内的属性定义在data中，注意是引号而不是花括号
2.	内联字符串拼接
```html
<a :herf=”‘http://’+addr”>跳转到百度</a>
```
```javascript
data:{
addr:”www.baidu.com”
}
```
3.	class绑定 
a.	对象语法：
a-1. v-bind:class="{prop1:isTrue,prop2:isActive}"，在data中要声明属性值(isTrue/isActive)为true或false，为true时才应用这个CSS class，为false时不应用;
a-2. 声明对象名，在data中声明属性并指定是否可用：v-bind:class=”classObj”,在data中声明classObj:{class1:true, class2:false}。则只应用class1;
b.	数组语法：
b-1. 声明数组名，在data中定义需要的数组元素；所有数组元素都会被应用；
b-2. 声明数组并定义其元素，在data中定义元素是否可用：
```
v-bind:class=”[class1,class2,class3]”   data中{class1:’class1’, class2:’class2’,class3:false}则只会应用class1和class2这两个类。
```
b-3. 声明数组和条件表达式，在data中定义条件表达式的值
4.	绑定内联样式
a.	对象语法：
在template中声明属性，在data中定义对应的属性值
```
v-bind:style=”{background:color, fontSize:fontSize+’px’}”
data:{color:’green’, fontSize:25}
```
b.	数组语法：
```
v-bind:style="[prop1,prop2]"
data:{ prop1:{background:'green'}, prop2:{fontSize:’25px’,fontWeight:’bold’}}
```
c.	多重值绑定：
可以为style绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 display: flex
`v-bind:style=”{display: [ ‘-webkit-box’, ‘-ms-flexbox’, ‘flex’ ]}”`

5. 动态参数
```html
<a v-bind:[attributeName]="url"> ... </a>
<!--如果你的 Vue 实例有一个 data 属性 attributeName，其值为 "href"，那么这个绑定将等价于 v-bind:href-->
<a v-on:[eventName]="doSomething"> ... </a>
<!--当 eventName 的值为 "focus" 时，v-on:[eventName] 将等价于 v-on:focus-->
```


###### （12）v-model
用于在表单上创建双向数据绑定
`<input v-model=”name”></input>   data:{ name:’Tom’}`
v-model修饰符
<1> .lazy (v-model.lazy)
默认情况下，v-model同步更新，使用lazy修饰符后，转变为在change事件后再同步
<2> .number (v-model.number)
将用户输入值转化为数值类型
<3> .trim (v-model.trim)
自动过滤用户输入的首尾空格

###### （13）v-on
用于监听dom事件，然后执行某些操作，简写为@，v-on:click等价于@click。表达式可以是一个方法名
###### 事件修饰符
（1） .stop 防止事件冒泡，相当于js中的event.stopPropagation();
（2） .capture 与事件冒泡方向相反，事件捕获由外到内
（3） .once 只会触发一次
（4） .self 只会触发自己范围内的事件，不包含子元素
（5） .prevent 拦截默认事件，相当于js中的event.preventDefault()。例如可以阻止表单提交是页面刷新等浏览器默认行为
（6） .passive 执行默认方法。一般用在滚动监听，@scoll,@touchmove。因为在滚动过程中，移动每个像素都会产生一次事件，每次都使用内核线程查询prevent会使滑动卡顿，，我们可以通过passive将内核线程查询跳过，可以大大提高滑动的流畅度。

###### （13）自定义指令
`Vue.directive('指令名',{})`
* 第一个参数是指令名，不需要加`v-`修饰符，但是调用的时候需要加
* 第二个参数是一个对象，这个对象身上有一些指令相关的钩子函数，这些函数可以在对应的阶段执行相关的操作
```javascript
Vue.directive('指令名',{
bind: function(){//每当指令绑定到元素上的时候，会立即执行这个bind函数，只执行一次
//更改样式只需要写到bind中
},
inserted: function(el){表示元素插入到dom中的时候会执行
el.focus()
//每个函数第一个参数永远是el，表示被绑定了指令的那个元素，这个el参数，是一个原生的js对象，拥有元素js操作dom的方法
//与js相关的最好写在inserted中，防止Js行为不生效
},
update: function(){当VNode更新的时候，会执行update,可能会触发多次
}
})
```
钩子函数的参数
* el：第一个参数，绑定的dom元素
* binding :第二个参数
   * binding.name:指令名
   * binding.value:指令的绑定值
   * binding.expression:绑定值的字符串形式
###### 自定义私有指令
directives对象中
```javascript
directives:{
  'fontweight':{
    bind: function(el){
      el.style.fontWeight = 700
    }
  }
}
```
&emsp;
***
# 2.过滤器
### 1.过滤器调用时的格式
`{{data | 过滤器的名称(参数)}}`
| 是管道操作符
### 2.过滤器的定义方式
`Vue.filter('过滤器的名称',function(data){});`
* 过滤器中的function的第一个参数是要处理的数据(过滤器管道符前面传递过来的数据)，后面的参数是过滤器传过来的参数
* 可以调用多个过滤器，会依次调用
`{{msg | filter1 | filter2}}`
### 3.全局过滤器和私有过滤器
* 全局过滤器：`Vue.filter('filterName',function(){})`
* 私有过滤器：写在filters对象内：`filters:{ filter1(){}}`
* 优先调用私有过滤器

&emsp;
***
# 3.键盘修饰符
### 1.用法
* 为键盘事件绑定按键，点击按键时触发事件
例如 @keydown.enter="add",按下回车执行时间
### 2.按键修饰符
|按键修饰符|别名|
|-|-|
|.enter|回车|
|.tab|tab键|
|.delete|删除键|
|.esc|esc键|
|.space|空格键|
|.up|上|
|.down|下|
|.left|左|
|.right|右|
### 3.也可以使用键盘码
例如f2的键盘码为113，则@keydown.113="add"等价于@keydown.f2="add"
### 4.自定义全局按键修饰符
`Vue.config.keyCodes.f2 = 113`

&emsp;
***
# 4.vue的生命周期钩子函数
### 1.什么是生命周期
从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期。别名也叫生命周期钩子。
### 2.主要的生命周期函数分类
- 创建期间

  - beforeCreate：创建之前。实例刚在内存中被创建出来，此时，data和methods还没有初始化好；
  - created：创建后。可以操作data和调用methods的最早阶段，此时模板还未被编译；
  - beforeMount：挂载之前。开始编译模板，在内存中生成一个编译好的模板字符串，渲染为内存中的dom。此时，只是在内存中渲染好了模板，并没有把模板挂载到页面中去；
  - Mounted：挂载后。将模板挂载到页面，完成真实的渲染。创建阶段结束。
- 运行期间

  - beforeUpdate：更新前。data改变才会触发。data更新，页面还未更新，页面和数据还未同步。
  - updated：更新后。data改变才会触发。data更新，页面也更新了，页面和数据同步了。
- 销毁期间

  - beforeDestory：销毁前。实例身上所有的data，methods,filters,directives...都还处于可用状态，实例还未被销毁。
  - destoryed：销毁后。组件已经被完全销毁了。组件中所有的东西都不可用了。


&emsp;
***
# 5.使用vue-resource发起get,post,jsonp请求
要先引入vue-resource.js
```javascript
//get请求
this.$http.get('url',{}).then(function(result){
  console.log(result.body);
})

//post请求  表单格式：application/x-www-form-urlencoded
//通过第三个参数设置提交的格式
this.$http.post('url',{},{ emulateJSON:true }).then(result => {
  console.log(result);
})

//jsonp请求
this.$http.jsonp('url',{}).then(result => {
  console.log(result.body);
})
```
- 全局配置
##### 1.接口请求的根域名
```javascript
Vue.http.options.root = 'http://localhost:8080/'
this.$http.get('api/getUserInfo').then() //注意此时url的api前面不能加/,否则不会启用根路径做拼接
```
##### 2.全局启用emulateJSON
` Vue.http.options.emulateJSON = true `

&emsp;
***
# 6.vue中的动画
### 1.使用过渡类名来实现动画
（1）使用`transition`元素，把需要被动画控制的元素包裹起来
（2）自定义两组样式来控制transition内部的元素来实现动画
```css
.v-enter,   /*进入之前，元素状态*/
.v-leave-to{     /*离开之后，终止状态*/
    transform: translateX(150px);
}

.v-enter-active,   /*入场动画的时间段*/
.v-enter-active{    /*离场动画的时间*/
    transition: all 0.4s ease;
}
```
缺点：所有过渡动画都共享这一套样式，所以要自定义v-前缀
### 2.自定义过渡动画样式的v-前缀，使其只应用在指定transition元素上
（1）`transition`元素加上name属性；
（2）把样式中的v-替换成name的值
```html
<transition name='my'></transition>
```
```css
.my-enter,.my-leave-to{}
.my-enter-active,.my-leave-active{}
```
### 3.使用第三方类来实现动画
例如使用animate.css来实现
```html
<link href='./animate.css'>
<!-- 入场动画使用bounceIn 出场动画使用bounceOut-->
<!-- 使用:duration="毫秒值"来统一设置入场和离场的动画时长-->
<!-- 使用:duration="{enter：n ,leave：n }"来分别设置入场和离场的动画时长-->
<transition 
  enter-active-class="animated bounceIn" 
  leave-active-class="animated bounceOut" 
  ：duration='{ enter:200,leave:400}'
 >
<h3 v-if="flag">动画标题</h3>
</transition>
```
###  4.钩子函数实现半场动画
小球的半场动画
```html
<div id="app" class="div">
  <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
  >
    <div class="ball" v-show="flag"></div>
  </transition>
  <input type="button" value="快到碗里来" @click="flag=!flag" style="position: absolute;top: 150px;left: 50px">
</div>
```
```css
.ball{
  width: 15px;
  height: 15px;
  background-color: red;
  border-radius: 50%;
}
```
```js
<script>
var vm = new Vue({
  el:'#app',
  data:{
    flag:false
  },
  methods:{
    //el表示要执行动画的那个DOM元素
    beforeEnter(el){ //动画入场之前，可以设置元素动画起始之前的样式
      el.style.transform = "translate(0,0)"
    },
    enter(el,done){  //动画开始之后的样式
      el.offsetWidth  //如果不写没有动画效果 el.offsetHeight/el.offsetWidth/el.offsetLeft/el.offsetRight都可以
      el.style.transform = "translate(50px,150px)"
      el.style.transition = "all 1s ease"
      done()
    },
    afterEnter(el){
      this.flag = !this.flag
    }
  }
})
</script>
```
### 5.使用transition-group元素实现列表添加删除动画
- 用v-for循环出来的必须用这个transition-group来实现动画
- 要为v-for循环的元素设置动画，必须写`:key`
- 给transition-group添加appear属性，能实现页面展示出来的时候的入场动画
- transition-group默认解析为span便签,span下面放ul不合理，所以用`tag="ul"`来指定transition-group解析为ul标签
```html
<transition-group appear tag="ul">
  <li v-for="item in list" :key="item.id">{{item.name}}</li>
</transition-group>
```
```css
    .v-enter,
    .v-leave-to{
        opacity: 0;
        transform: translateY(80px);
    }

    .v-enter-active,
    .v-leave-active{
        transition: all 1s ease;
    }

    .v-move{
        transition: all 1s ease;
    }
    .v-leave-active{
        position: absolute;
    }
```

&emsp;
***
# 7.组件
- 模块化：是从代码逻辑的角度来划分的；方便代码分层开发，保证每个功能模块的职能单一
- 组件化：是从UI界面的角度进行划分的，前端的组件化，方便UI组件的重用

### 1.创建全局组件
#### （1）Vue.extend + Vue.component
1. Vue.extend创建组件，返回的是一个组件对象，template属性指定了要显示的HTML模板
2. Vue.component第一个参数是组件名，第二个参数是组件对象，用1中的
3. 在html中以标签的形式引入组件。标签名为组件名

```js
var myComponent = Vue.extend({
  template: '<div>这是一个div</div>'
})
Vue.component('my-component',myComponent)
```
```html
<my-component></my-component>
```

也可以简写：
```js
Vue.component('my-component',Vue.extend({
  template: '<div>这是一个div</div>'
}))
```
#### (2)Vue.component
```js
Vue.component('my-component',{
  template:'<div><h3>标题</h3><p>段落</p></div>'  //注意：只能有一个根标签
})
```
#### (3)抽离template，有点脚手架的味道了
```js
Vue.component('my-coponent',{
  template:'#teml'
})

```
```html
<!--在html中写模板结构，指定id-->
<template id="teml">
  <div>
  <h1>标题</h1><p>段落</p>  <!--只能有一个根标签-->
  </div>
</template>
<!--引用模板-->
<div id="app">
  <my-component></my-component>
</div>
```
### 2.创建私有组件（在vue实例的components对象中定义）
```js
  components:{
  login: {
    template:'<h1>这是login私有组件</h1>'
  }
  }
  //可以简写
  components:{
  login
  }
```
 只能在对应vue实例中使用
 也可以参照上一小节抽离template
### 3.组件中的data
- 组件中的data与实例中的data不同，必须是一个带返回值的函数，应该这样写
```js
data(){
  return {
    msg:'这是组件中的data'
  }
}
```
- 为啥组件中的data必须要返回值
不使用return包裹的数据会在项目的全局可见，会造成变量污染；使用return包裹后数据中变量只在当前组件中生效，不会影响其他组件。

### 4.组件切换
#### (1)v-if和v-else结合flag进行组件切换
#### (2)用vue的component元素实现组件切换
- component是一个占位符，:is属性指定了要展示的组件名
`<component :is="'componentName'"></component> <!--注意组件名是字符串-->`
代码实现：
```html
  <input type="button" value="组件1" @click="componentName='component1'">
  <input type="button" value="组件2" @click="componentName='component2'">
  <input type="button" value="组件3" @click="componentName='component3'">
  <compontent :is="componentName"></compontent>
```
```js
  Vue.component('component1',{
    template:'<div style="width: 1000px;height: 300px;background-color: pink">组件1</div>'
  })
  Vue.component('component2',{
    template:'<div style="width: 1000px;height: 300px;background-color: #86ffa3">组件2</div>'
  })
  Vue.component('component3',{
    template:'<div style="width: 1000px;height: 300px;background-color: #11c4ff">组件3</div>'
  })
  var vm = new Vue({
    el:'#app',
    data:{
      componentName:'component1' //默认显示组件1
    }
  })
```
#### (3)组件切换动画
- 还是用transition标签，mode属性可以设置切换时候的模式
- css要定义.v-enter,.v-leave-to{}和.v-enter-active,.v-leave-active{}两组样式
```html
<transition mode="out-in">
<component :is="componentName"></component>
</transition>
```

### 5.组件传值
#### (1)父组件向子组件传值
- 默认情况下子组件是访问不到父组件中的data值和methods方法的
- 属性绑定+props申明
```html
<!--先属性绑定-->
<my-component :parentmsg="msg"></my-component>  <!--msg是父组件上的data数据-->
```
还要在子组件的props数组申明一下接收到的数据的名字
```js
components:{
  myComponent:{
    template:'<h1>{{parentmsg}}</h1>',
    props:['parentmsg']
  }
}
```
- props中的数据，都是父组件传递给子组件的，只读，无法重新赋值
#### (2)父组件向子组件传递方法(子组件调用父组件方法)
- 事件绑定+methods数组中调用
```html
<!--先事件绑定-->
<my-component @func="show"></my-component>  <!--show方法是父组件上的方法-->
```
然后在子组件的methods数组通过this.$emit('func')来调用
```js
template:'<div><button @click="show">点击</button></div>', /*show这个方法名随意，与父组件无关*/
methods: {
  show(){
    this.$emit('func')  //this是当前子组件，$emit()代表触发，参数为函数名字符串。若要传参，接着在第二个参数位置写
  }
}
```
#### (3)由2就可以引申出子组件向父组件传值
```html
<div id="app">
  {{msgFromSon}}
  <my-component @func="show"></my-component>  <!--show()不带参数-->
</div>
```
```js
var vm = new Vue({
  el:'#app',
  data:{
    msgFromSon:null
  },
  methods:{
    show(data){
      this.msgFromSon = data;
  }
},
components:{
  myComponent:{
    template:'<div><button @click="show">子组件向父组件传值</button></div>',
    data(){
      return {
        msg: '子组件上的msg'
      }
    },
    methods: {
      show(){
        this.$emit('func',this.msg)
      }
    }
  }
}})
```
#### (4)父组件调用子组件的data和msg：见下一节$refs
### 6.使用ref获取dom元素和组件的引用(vue不推荐直接操作dom)
- 在vue实例上有一个$refs对象，保存了指定ref值的dom对象
- 可以在dom元素上指定ref值(ref="btn")，然后通过this.$refs.btn获取这个dom元素
```html
<p ref="text">这是一个文本<p>
<button @click="getText">获取p标签的文本值</button>
```
```js
methods:{
  getText(){
    console.log(this.$refs.text.innerText)
  }
}
```
- 同理，组件也可以使用ref来获取到。例如有个子组件的ref指定为"myComponment",data里有个msg，methods里面有个show()
- 那么通过父组件通过this.$refs.myComponent.msg就可以获取到子组件的数据
- 通过this.$refs.myComponent.show()可以调用子组件的方法


&emsp;
***
# 8.路由
- 前端通过hash(#)来实现路由
### 1.vue-router的基本使用
- 当导入了vue-router包之后，就有了一个路由的构造函数VueRouter
- routes是路由匹配规则
- 每个路由匹配规则都是一个对象，有两个必须的属性，path和component
- path表示监听哪个路由链接地址，component表示路由匹配path时显示component对应的组件
- `<router-view></router-view>`做路由挂载
- ` <a href="#/login">登陆</a>     <a href="#/register">注册</a>`可以跳转。这样也可以实现组件切换
- 也可以使用`<router-link to="/login">登录</router-link>`来做路由跳转，默认渲染为a标签，若要渲染为其他，加tag。要设置选中路由的样式则设置.router-link-active
- 路由切换若要使用动画，可以用transition把router-view包起来
```js
var routerObj = new VueRouter({
  routes:[ 
  {path:'/',redirect:'login'},/*根路径默认显示login组件*/
  {path:'/login',component:login},
  {path:'/register',component:register}
  ],
  linkActiveClass:'myactive' //链接激活时的样式，默认是.router-link-active
})
/*将router注册到vue实例*/
var vm = new Vue({
  router:routerObj
})
```
### 2.路由传参
#### (1)$route.query
传值:
`<router-link to="/login?id=10"></router-link>`
取值:
`this.$route.query.id`
#### (2)$route.params
传值:
```js
routes:[
  {path:'/login/:id/:name',component:login}
]
```
```html
<router-link to="/login/10/陈俊"></router-link>
```
取值:
`this.$route.params.id,this.$route.params.name`

### 3.路由嵌套(chirdren)
```html
<router-link to="/account/login">登录</router-link>
<router-view></router-view>
```
```js
routes:[
{
  path:'/account',
  component:account,
  children:[
    {path:'login',component:login}  //login前面不加/
  ]
}
]
```
### 4.命名视图
- router-view加name
使用命名视图实现经典布局
```html
<router-view></router-view>
<router-view name="leftBox"></router-view>
<router-view name="mainBox"></router-view>
```
```js
var router = new VueRouter({
  routes:[
    {path:'/',components:
      { //记住这里是对象
        'default':header,
        'leftBox':leftBox,
        'mainBox':mainBox
      }
    }
  ]
})
```

&emsp;
***
# 9.watch
### 1.监听属性值变化
- 可以监听data中指定数据的变化，然后触发watch对象中对应的function函数
```js
watch:{
  msg:function(){   //当data上的msg变化时会执行函数
    console.log('监视到了msg的变化')
    }
}
```
### 2.监听路由变化
```js
watch:{
  '$route.path':function(newVal,oldVal){
      console.log(oldVal+'->'+newVal)
  }
}
```

&emsp;
***
# 10.computed计算属性
- 在computed对象中可以定义一些属性，这些属性叫做[计算属性],本质是一些方法。只不过调用的时候直接当做属性来用。
- 只要计算属性函数内部调用的data数据发生改变，就会重新计算这个计算属性的属性。
- 计算属性的求值结果会被缓存起来。
- 计算属性函数调用的data数据时不可简写为箭头函数，因为箭头函数的this指向会继承父级作用域的上下文，此时指向的是window而不是vue实例
```html
<input type="text" v-model="firstname"/>+
<input type="text" v-model="lastname"/>=
<input type="text" v-model="fullname"/>
<p>{{fullname}}</p>
```
```js
data:{
  firstname:'',
  lastname:''
},
computed:{
  fullname: function () {
    return  this.firstname +"-"+ this.lastname
  }
}
```
- 计算属性的setter和getter（默认只有getter，可以设置setter）
```js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
// 运行 vm.fullName = 'John Doe' 时，setter 会被调用，vm.firstName 和 vm.lastName 也会相应地被更新。
```
