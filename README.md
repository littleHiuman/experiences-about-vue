# experiences-about-vue
vue项目的一些心得。

---
vuex 状态

vue-cli 命令行

vue vue

vue-router 路由

es6

eslint

---
**Js写法 规范。**

**eslint常见问题**



brace-style？

no-sequences？

block-spacing？



比较时，使用全等号

所有的switch语句都必须要有一个default分支

yoda：yoda条件语句就是对象字面量应该写在比较操作符的左边，而变量应该写在比较操作符的右边（默认的规则要求，变量写在左边而字面量写在右边）


个别符号以及关键字之间需要空格（比如function，逗号，大括号，运算符）

逗号在行尾出现/行首

不以新行开始的块 { 前面要不要有空格



立即调用函数的写法：

```
(function() {
  // body 
}());
```

只能使用单引号

最后必须有一行空行，

不能有多余空行

不能有多余空格

空位/制表符距离为2

可以设置带分号，否则js中不能带分号。

```"semi": [2, "always"]```

不能 定义了却未使用的变量

alias中定义的简称只能用于js部分。

模块必须有一个根元素

整个页面有切换动画，那么页面的根元素不能有其他样式影响

Vue实例中 最后一个属性末不需要加逗号

对象里的最后一项，不需要加逗号

---
**引入css文件：**

1. index.html中引入，

2. <style></style>中引入，需要@import，

或者另外一个<style src=""></style>

3. main.js中引入需要写loader（inport/require）

```
require('!style-loader!css-loader!less-loader!./assets/css/common_m.less')
```

---
**cssloader：**

```
{
　　test: /\.css$/,
　　loader: "style-loader!css-loader",
},
{
　　test: /\.less$/,
　　loader: "style-loader!css-loader!less-loader",
},
```

---
<router-view></router-view>与写的位置无关

---
path.join(__dirname,'..');

---
this.$set(this, '属性', '值')

---
css scoped 仅本组件

---
对象可以存图片。使用require即可。

```
images: {
　　error: require('./toast-error.png'),
　　success: require('./toast-success.png'),
　　load: require('./toast-load.gif'),
　　waiting: require('./toast-hourglass.svg')
}
```

---
border。各屏幕分辨率不同出现的粗细问题。

公共部分。写成组件。利用传参改变样式/内容。

Ajax。axios。

能用data数据解决的问题，不用方法解决。如取反。长度。是否空/false/true。

v-bind:style src to ...

---
路由传参。$route。

历史记录切换。router-link to/:to或者router.push()/router.replace()



#router.push(location) 导航到不同的 URL

```
// 声明式
<router-link :to="...">

// 编程式
router.push(...)

// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: 123 }})

// 带查询参数，变成 /register?plan=private

router.push({ path: 'register', query: { plan: 'private' }})
```

---
#router.replace(location) 它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录。

```
// 声明式
<router-link :to="..." replace>

// 编程式
router.replace(...)
```

---
#router.go(n) 在 history 记录中向前或者后退多少步，类似 window.history.go(n) 值可以正可以负

**综合使用**

```
const router = new VueRouter({
　　routes: [
　　　　{
　　　　　　path: '/user/:userId',
　　　　　　name: 'user',
　　　　　　component: User
　　　　}
　　]
})

<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

router.push({ name: 'user', params: { userId: 123 }})
```

这两种方式都会把路由导航到 /user/123 路径。

---
**命名视图**

https://router.vuejs.org/zh-cn/essentials/named-views.html

https://jsfiddle.net/posva/6du90epg/

有时候想同时（同级）展示多个视图，而不是嵌套展示，例如创建一个布局，有 sidebar（侧导航） 和 main（主内容） 两个视图，这个时候命名视图就派上用场了。

你可以在界面中拥有多个单独命名的视图，而不是只有一个单独的出口。如果 router-view 没有设置名字，那么默认为 default。

```
<router-view class="view one"></router-view>

<router-view class="view two" name="a"></router-view>

<router-view class="view three" name="b"></router-view>
// 一个视图使用一个组件渲染，因此对于同个路由，多个视图就需要多个组件。确保正确使用 components 配置（带上 s）：

const router = new VueRouter({
　　routes: [
　　　　{
　　　　　　path: '/',
　　　　　　components: {
　　　　　　　　default: Foo,
　　　　　　　　a: Bar,
　　　　　　　　b: Baz
　　　　　　}
　　　　}
　　]
})
```

---
重定向 和 别名


切换时清空历史记录。数据丢失。sessionStorage。

相对路径。

append。

渲染成某个标签。tag

可以在router-link内嵌套其他内容。

---
类型都是Object

$route.params（一个 key/value 对象，包含了 动态片段 和 全匹配片段，如果没有路由参数，就是一个空对象。）

$route.query（一个 key/value 对象，表示 URL 查询参数。例如，对于路径 /foo?user=1，则有 $route.query.user == 1，如果没有查询参数，则是个空对象。）

```
<div>
    <router-link :to="{ name: 'Hello' , params: { userId: 123 }}">
        click1
    </router-link>
</div>

<div>
    <router-link :to="{ path: 'hello' , query: {show: 2}}">
        click2
    </router-link>
</div>

console.log(this.$route.params.userId)

console.log('top is params, bottom is query')

console.log(this.$route.query.show)
```

---
watch：

```
watch: {
　　'$route' (to, from) {
　　// 对路由变化作出响应...
　　}
}
```

---
v-show v-if 。v-if为假直接不渲染。v-show为假display none。

当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级。

外容器overflow hidden，内容器overflow scroll。

---
**过渡效果：**

```
<transition name="fade"></transition>

.fade-enter-active, .fade-leave-active {
　　-webkit-transition: opacity .7s;
　　transition: opacity .7s;
}

.fade-enter, .fade-leave-active {
　　opacity: 0
}
```

---
路由钩子 判断从哪个路由过来，到哪个路由。然后跳转到哪个路由。（全局钩子。局部钩子。）

component页面内也可以监听路由。

---
滚动行为。历史记录之间切换。页面位置。返回对象。

```
scrollBehavior (to, from, savedPosition) {
　　return { x: 0, y: 0 }
}
```

---
锚点的实现。通过scrollTop。

路由元信息。路由嵌套。

---
懒加载。

4、在异步加载页面中载嵌入异步加载的组件时对页面是否会有渲染延时影响？

答：会， 异步加载的组件将会比页面中其他元素滞后出现， 页面会有瞬间闪跳影响；

解决方案：因为在首次加载组件的时候会有加载时间， 出现页面滞后， 所以需要合理的进行页面结构设计， 避免首次出现跳闪现象；

At all:

　　1、路由页面以及路由页面中的组件全都使用懒加载

　　优点：（1）最大化的实现随用随载

　　　　　（2）团队开发不会因为沟通问题造成资源的重复浪费　　　　

　　缺点：（1）当一个页面中嵌套多个组件时将发送多次的http请求，可能会造成网页显示过慢且渲染参差不齐的问题

　　2、路由页面使用懒加载， 而路由页面中的组件按需进行懒加载, 即如果组件不大且使用不太频繁, 直接在路由页面中导入组件, 如果组件使用较为频繁使用懒加载

　　优点：（1）能够减少页面中的http请求，页面显示效果好

　　缺点：（2）需要团队事先交流， 在框架中分别建立懒加载组件与非懒加载组件文件夹

　　3、路由页面使用懒加载，在不特别影响首页显示延迟的情况下，根页面合理导入复用组件，再结合方案2

　　优点：（1）合理解决首页延迟显示问题

　　　　　（2）能够最大化的减少http请求， 且做其他他路由界面的显示效果最佳

　　缺点：（1）还是需要团队交流，建立合理区分各种加载方式的组件文件夹
  
---

```
export default new Router({
　　routes: [
　　　　{
　　　　　　path: '/',
　　　　　　component: resolve => require(['components/Hello.vue'], resolve)
　　　　},
　　　　{
　　　　　　path: '/about',
　　　　　　component: resolve => require(['components/About.vue'], resolve)
　　　　}
　　]
})
```　　

// solve：
// components/page

---
<keep-alive> 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 <transition> 相似，<keep-alive> 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。

当组件在 <keep-alive> 内被切换，它的 activated 和 deactivated 这两个生命周期钩子函数将会被对应执行。

主要用于保留组件状态或避免重新渲染。

---
 组件：

当注册组件（或者 props）时，可以使用 kebab-case ，camelCase ，或 TitleCase 。Vue 不关心这个。

```
// 在组件定义中

components: {

　　// 使用 kebab-case 形式注册
　　'kebab-cased-component': { },

　　// register using camelCase
　　'camelCasedComponent': { },

　　// register using TitleCase
　　'TitleCasedComponent': { }
}

<!-- 在HTML模版中始终使用 kebab-case 形式 -->

<kebab-cased-component></kebab-cased-component>

<camel-cased-component></camel-cased-component>

<title-cased-component></title-cased-component>

// 当使用字符串模式时，不受 HTML 的 case-insensitive 限制。

<!-- 在字符串模版中可以用任何你喜欢的方式! -->

<my-component></my-component>

<myComponent></myComponent>

<MyComponent></MyComponent>
```

---
如果组件未经 slot 元素传递内容，你甚至可以在组件名后使用 / 使其自闭合：

<my-component/>

当然，这只在字符串模版中有效。因为自闭的自定义元素是无效的 HTML ，浏览器原生的解析器也无法识别它。

---
**component命名要求：**

1. 检查名称是否与 HTML 元素或者 Vue 保留标签重名，不区分大小写。（常用HTML标签）

2. 检查组件名称是否以字母开头，后面跟字母、数值或下划线。

---
使用 Virtual DOM 解析模板时，不会将模板中的标签名转成小写，而是保留原始标签名。然后，使用原始的标签名进行匹配组件。

例如， <MyComponent></MyComponent> 不会转为为小写形式，直接以 MyComponent 为基础开始匹配。

当然，匹配的规则依次匹配：原标签名、camelCase化的标签名、PascalCase化的标签名。

```
//之前在 1.0 不能正常运行的示例代码，在 2.0 中可以正常运行了：

Vue.component('MyComponent', {
　　template: '<div>hello, world</div>'
})

new Vue({
　　el: '#app',
　　template: '<MyComponent></MyComponent>'
})
```

---
在 Vue 1.0 和 2.0 中还有一种定义组件模板的方式，即使用 DOM 元素。在这种情况下，解析模板时仍然会将标签转为小写形式。所以下面的代码，在 1.0 和 2.0 均不能正常运行。

```
// index.html

<div id="app">
　　<MyComponent></MyComponent>
</div>

// main.js
Vue.component('MyComponent', {
　　template: '<div>hello, world</div>'
})

new Vue({
　　el: '#app'
})
``` 

---
由于 JavaScript 的限制， Vue 不能检测以下变动的数组：

```
// 当你利用索引直接设置一个项时，例如
vm.items[indexOfItem] = newValue

// 当你修改数组的长度时，例如：
vm.items.length = newLength
```


为了解决第一类问题，以下两种方式都可以实现和 vm.items[indexOfItem] = newValue 相同的效果， 同时也将触发状态更新：

```
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)

// Array.prototype.splice`
example1.items.splice(indexOfItem, 1, newValue)
```


为了解决第二类问题，你也同样可以使用 splice：

```
example1.items.splice(newLength)
```

---
父组件给子组件传参，通过props属性。还可以定义类型

https://cn.vuejs.org/v2/guide/components.html#Prop-验证

除了以下定义一种类型的写法，还有多种类型，必传且是某个类型，某个类型且有默认值，某个类型但默认值由一个工厂函数返回，或者是自定义
```
props: {
  username: String,
}

// 全局注册的组件的写法：
props: ['myMessage'],
```

子组件给父组件传参，通过this.$emit('方法', '内容')

---
vertical-align: top;
两个span对齐 / 图片和文字对齐 / inline-block元素 .......

---
字体图标。

---
一行文字超出省略号：

```
white-space: nowrap

overflow: hidden

text-overflow: ellipsis
```

---
空白间隙去掉的方法：

```
font-size: 0;

// 或者 两个标签之间紧贴着。
```

---
filter类似滤镜效果。模糊效果。

```
filter: blur(10px)
```

同上类似。模糊效果（仅对背景生效，仅限iOS系统）

```
backdrop-filter: blur(10px)
```

---
type，给参数 / 变量定义类型。

---
computed，内容变时会更新，否则会缓存起来。

如果是传参等方式得到值，需要判断值是否为空，否则会报值为undefined的错。

---
使用变量 / 常量拼接内容，而不使用字符串拼接内容。

---
各子元素不固定宽 / 高，但是整个布局占固定值时，flex布局。尽量用block元素。

flex的默认值为0 1 auto

flex是放大比例（flex-grow） 缩小比例（flex-shrink）占据的空间（flex-basis）的简写属性

可以填auto（相当于 1 1 auto）和none（0 0 auto）

flex: 1（相当于 1 1 0%）

使用flex属性后，该元素最好添加width属性，值为flex-basis定义的值。 如：flex: 0 0 100px;

---
vue项目中，不用写兼容性代码。

因为vue-loader在编译.vue文件的时候，使用了Postcss的工具，它会给有兼容性问题的属性添加兼容性代码。

它是根据can i use官网写的代码。

写在<style></style>内才会生效。在html中添加style属性是不会添加兼容性代码的。

---
换行问题：

v-html可以直接加<br>进行换行，v-model中无效

例外：textarea标签使用v-model时，可以使用\r进行换行

---
实现垂直居中的方式：

父元素： display: table，

子元素： display: table-cell;vertical-align: middle;
无论一行或多行。

---
删除线效果 text-decoration: line-through

---
iScroll

---
ref的使用：

在父页面调用子组件的标签：

在父页面中的组件上加ref。然后在子组件中的某个标签加ref。即可。

---
nextTick

将回调延迟到下次 DOM 更新循环之后执行。

https://cn.vuejs.org/v2/api/#vm-nextTick

```
new Vue({
  // ...
  methods: {
    // ...
    example: function () {
      // 修改数据
      this.message = 'changed'
      // DOM 还没有更新
      this.$nextTick(function () {
        // DOM 现在更新了
        // `this` 绑定到当前实例
        this.doSomethingElse()
      })
    }
  }
})
```

---
```box-sizing: border-box```

---
:disabled="type == '值'"

---

