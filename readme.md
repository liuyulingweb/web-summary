### 前端知识概编

#### vue 专场 1

1.  ##### [6 条 vue 实例的 属性](https://www.jianshu.com/p/fdf8dd36c78f)

    1.  vm.$data
    2.  methods
    3.  computed
    4.  vm.$props
    5.  vm.$el
    6.  vm.$root
    7.  vm.$options
    8.  vm.$parent
    9.  vm.$children
    10.  vm.$slots
    11.  vm.$refs

2.  [6 个 vue 指令 分别说明什么意思](https://www.jianshu.com/p/c4a87e1b4ef7)

    1.  v-text	v-text主要用来更新textContent

        `<span v-text="msg"></span> 等价于 <span>{{msg}}</span>`

    2.  v-html	为了输出真正的HTML

    3.  v-pre

        ```html
        <!-- 若不加v-pre指令，直接编译会报错，因为data中没有a和b属性 -->
        <div v-pre>
        {{a}} + {{b}}
        </div>
        ```

    4.  v-once	v-once关联的实例，只会渲染一次。

    5.  v-if	可以实现条件渲染

    6.   v-else	v-else是搭配v-if使用的，它必须紧跟在v-if或者v-else-if后面，否则不起作用。

    7.  v-else-if	v-else-if充当v-if的else-if块，可以链式的使用多次。

    8.  v-show	简单的切换css的dispaly属性。

        >   注意：v-if有更高的切换开销
        >   v-show有更高的初始渲染开销。
        >   因此，如果要非常频繁的切换，则使用v-show较好；如果在运行时条件不太可能改变，则v-if较好

    9.  v-for	用v-for指令根据遍历数组来进行渲染

    10.  v-bind	动态的绑定一个或者多个特性,常用于动态绑定class和style。以及href等。简写为一个冒号。

    11.   v-model	指令用于在表单上创建**双向数据绑定**。

         >   **v-model修饰符**
         >
         >   **<1> .lazy**
         >
         >   **<2> .number**
         >
         >   **<3> .trim**

    12.  v-on

         v-on主要用来监听dom事件，以便执行一些代码块。简写为@

3.  说一下vue 如何实现数据双向绑定  底层原理 

    vue数据双向绑定是通过数据劫持结合发布者-订阅者模式的方式来实现的，有两个相对应的get和set方法，通过Object.defineProperty(obj, prop, descriptor)来实现数据劫持的。针对属性，我们可以给这个属性设置一些特性，比如是否只读不可以写；是否可以被for..in或Object.keys()遍历。

4.  [vue 属性 data computed watch 这三个属性的区别](https://blog.csdn.net/dkr380205984/article/details/79361861)  

    data是静态数据设置，没有缓存。
    computed是动态数据设置，具有缓存。（依赖值）
    watch是数据监听，实时改变数据。

5.  说一下 什么 变异数组和非变异数组  以及  可变对象 和 不可变对象  

    变异数组：可以改变元素组(会改变被这些方法调用的原始数组)

    -   push( )末尾添加
    -   pop( )删除数组最后一个并返回
    -   shift( )删除数组第一个并返回
    -   unshift( )可向数组的开头添加一个或更多元素，并返回新的长度
    -   splice(index,howmany,item1,.....,itemX ) 向/从数组中添加/删除项目，然后返回被删除的项目
    -   sort( )
    -   reverse( )

    非变异数组：不可以改变元素组，返回新数组

    -   filter( )
    -   concat( )
    -   slice( )

    可变对象：Array，object。数据会改变，但不会监听到

    不可变对象：string，number，布尔

6.  vue 如何实现 深度监听 以及什么时候需要用到深度监听

    如何实现：watch深度监听利用handel，deep，immediate:true代表如果在 wacth 里声明了 firstName 之后，就会立即先去执行里面的handler方法
    什么时候：在有可变对象的时候需要用到深度对象 

7.  vue 组件生命周期 分为几个阶段（4个）  有哪些（8个）生命周期钩子函数

    ```js
    beforeCreate: function(){
        console.log(this);
        showData('创建vue实例前',this);
    },
    created: function(){
        showData('创建vue实例后',this);
    },
    beforeMount:function(){
        showData('挂载到dom前',this);
    },
    mounted: function(){
        showData('挂载到dom后',this);
    },
    beforeUpdate:function(){
        showData('数据变化更新前',this);
    },
    updated:function(){
        showData('数据变化更新后',this);
    },
    beforeDestroy:function(){
        vm.test ="3333";
        showData('vue实例销毁前',this);
    },
    destroyed:function(){
        showData('vue实例销毁后',this);
    }
    ```

     ![](https://ws2.sinaimg.cn/large/006tNc79ly1g03wzylol0j30ev0g63yz.jpg)

8.  vue 如何绑定事件 绑定变量 绑定属性   

    绑定事件：v-on
    绑定变量：{{}}
    绑定属性：v-bind

9.  [vue slot 具体用法  你项目怎么使用slot](http://www.php.cn/js-tutorial-402748.html)

    封装组件使用slot分发不同信息
    可以通过具名插槽来精确的分发到指定位置 

    ` <slot name="my-header">头部默认值</slot>`

    ` <p slot="my-header">我是头部</p>`

10. vue 如何动态切换组件 说出所有的具体实现方法  

    利用v-if v-show 
    利用路由
    利用slot
    [利用component组件is属性](https://cn.vuejs.org/v2/guide/components-dynamic-async.html)

11. data 和 \$data   watch 和 vm.$watch 的 区别  [以及如何校验 props](https://www.cnblogs.com/exhuasted/p/7250452.html) 

    Vue实例会代理`data`对象的属性, `vm.$data.a`相等于`vm.a`,**以-和$开头的属性不会被代理，因为这会和Vue的内部属性和API冲突**。

    如何校验 props ：可以使用type来声明这个参数可以接受的数据的类型，当检查规则只有一个的时候type可以略写

    >   一个综合的例子
    >
    >   ```js
    >   props: {
    >       // fooA只接受数值类型的参数
    >       fooA: Number,
    >       // fooB可以接受字符串和数值类型的参数
    >       fooB: [String, Number],
    >       // fooC可以接受字符串类型的参数，并且这个参数必须传入
    >       fooC: {
    >           type: String,
    >           required: true
    >       },
    >       // fooD接受数值类型的参数，如果不传入的话默认就是100
    >       fooD: {
    >           type: Number,
    >           default: 100
    >       },
    >       // fooE接受对象类型的参数
    >       fooE: {
    >           type: Object,
    >           // 当为对象类型设置默认值时必须使用函数返回
    >           default: function(){
    >               return { message: 'Hello, world' }
    >           }
    >       },
    >       // fooF使用一个自定义的验证器
    >       fooF: {
    >           validator: function(value){
    >               return value>=0 && value<=100;
    >           }
    >       }
    >   }
    >   ```
    >
    >   

12. 补充：

    -   vue是什么
        1.  一套用于构建用户界面的**渐进式框架**
        2.  可以自底向上逐层应用
        3.  核心库只关注视图层
        4.  与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)(单文件组件) 以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)(比如vuex）结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。


vue 专场 2   **************************************

1.  vue 如何自定义指令 如何自定义过滤器  自定义指令意义和自定义过滤器的意义

    自定义指令：使用Vue.directive(id,definition)注册全局自定义指令，使用组件的directives选项注册局部自定义指令。
    自定义指令意义：对普通 DOM 元素进行底层操作
    自定义过滤器：通过filters
    自定义过滤器的意义：实现数据的筛选、过滤、格式化

2.  vue 定义创建路由 的步骤 

    如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

    定义路由组件

    定义路由 routes 路由配置 path,component

    创建 router 实例，然后传 `routes` 配置
    挂载到根实例
    路由出口  路由匹配到的组件将渲染在这里
    页面导航 to 属性

3.  vue 如何定义嵌套路由 以及 vue 路由如何去 # 号，还有 Vue.use(VueRouter) 中 Vue.use 的作用

    vue [如何定义嵌套路](https://www.cnblogs.com/yuwenjing0727/p/7097674.html)：children

     [去#](https://www.cnblogs.com/libo0125ok/p/9593741.html)：将mode改为history（需要配置服务器，不然无法刷新)
      Vue.use将可以在全局使用到该模块

4.  vue 父组件 去访问 通信 作用 子组件 方式有哪些 ?

    props，ref，空实例对象，vuex

5.  vue 子组件 去通信 父组件的 方式有哪些 ?  

    props，$parent，自定义事件，空实例对象，vuex

5.1  vue 如何实现自定义事件 

​	在父组件上定义事件（on），子组件帮助触发（$emit）。自定义发送一个

6.  vue 数据管理架构 vuex  的原理 

    由store，action，mutation，state四层结构通过单向数据流实现数据的集中式管理。

    https://vuex.vuejs.org/vuex.png

7.  vuex 里面 四个 辅助 函数  (mapState、mapGetters、mapMutations、mapActions  )

8.  vue 路由 里面 [路由守卫](https://blog.csdn.net/qq_37212162/article/details/81041665) 哪三种路由守卫? 什么作用 监听路由切换 各写一个路由守卫函数 

    3种，全局，基于路由，基于组件

    钩子函数：

    beforeRouteEnter 
    beforeRouteUpdate (2.2 新增) 
    beforeRouteLeave

9.  [比较说明 vue 设计模式  MVC MVVM MVP  三种设计模式  的 理解](https://blog.csdn.net/axi295309066/article/details/52596220) 

10. 你选择vue 框架的出发点是什么? vue开发中遇到过哪些比较棘手的问题 

    [选择原因](https://blog.csdn.net/binlety/article/details/81252874)：Vue.js是一个轻巧、高性能、可组件化的MVVM库，同时拥有非常容易上手的API。

    vue两大特点：响应式编程、组件化
    vue的优势：轻量级框架、简单易学、双向数据绑定、组件化、视图、数据和结构的分离、虚拟[DOM](https://www.baidu.com/s?wd=DOM&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)、运行速度快

    vue是单页面应用，使页面局部刷新，不用每次跳转页面都要请求所有数据和dom，这样大大加快了访问速度和提升用户体验。而且他的第三方ui库很多节省开发时间。

    [比较棘手的问题](https://blog.csdn.net/chen548246/article/details/84393347) ：

    1.  vue页面刷新 store中状态还原问题，解决办法：利用[sessionStorage](https://blog.csdn.net/goodaxuan/article/details/82113123)

11. this.$nextTick 使用过没? 具体用于什么场景  

    将回调延迟到下次 DOM 更新循环之后执行，相当于延时执行，一般使用在数据请求后回调渲染数据中

react 专场 1 

1.  react 和 react-native 的 区别    https://reactnative.cn/

    React 是基础框架，是一套基础设计实现理念，开发者不能直接使用它来开发移动应用或者网页。

    React.js在React框架之上，发展出了React.js 框架来开发网页。

    React Native：在React框架之上，发展出来React Native 用来开发移动应用。

2.  react 虚拟DOM 的理解 

    React会在内存中维护一个虚拟DOM树，对这个树进行读或写，实际上是对虚拟DOM进行。当数据变化时，React会自动更新虚拟DOM，然后将新的虚拟DOM和旧的虚拟DOM进行对比，找到变更的部分，得出一个diff，然后将diff放到一个队列里，最终批量更新这些diff到DOM中。

3.  react Diff 算法的 深入理解 

    [链接](https://blog.csdn.net/one_girl/article/details/81086289)

4.  [react Javascript XML 语法有什么特点](https://www.cnblogs.com/tomblog/p/4774432.html)  

    jsx 的特点：

    1.类xml语法易于理解。

    2.增强js语意。

    3.结构清晰。

    4.抽象程度高，易于跨平台。

    5.代码模块化。

5.  react props state context  三者的区别 

    `state`严格来说是内部状态或者说是局部状态

     `props`在组件中通讯比较常见的，用于父组件传递数据给子组件中，不能跨组件传递

    `context`是可以跨组件之间的传递

6.  [react 创建 组件 有哪些方式 ?](https://www.cnblogs.com/wonyun/p/5930333.html)   createClass Component function

    1.  函数式定义的`无状态组件`
    2.  es5原生方式`React.createClass`定义的组件
    3.  es6形式的`extends React.Component`定义的组件

7.  react 组件生命周期分为几个阶段,有那几个 常见的生命周期钩子函数 

    react 组件的生命周期
     	含义   组件从初始化渲染到被移除或者销毁的过程  成为组件的生命周期
     	1. 每个组件都有生命周期
     	2. react 通过组件的生命周期钩子函数来管理 组件
     	3. 系统 某些状态和参数发生改变的时候，系统立马去通知 对应处理的函数叫做钩子函数
    	 	hooks 钩子函数  允许在特定的时期添加用户自己的代码  不同的阶段添加自己的逻辑代码

     	react 组件的生命周期钩子函数 分为三个阶段 
     	1.mount  组件的初始化  从虚拟DOM 渲染成为真实DOM 的过程
     	2.update   组件的数据变化   组件的state 更新 导致二次渲染的过程
     	3.unmount  组件销毁   组件因为路由切换而销毁 (浏览器的垃圾回收机制 )

     	mounted 组件载入阶段  (钩子函数)
     	1.getDefaultProps   设置组件默认的props
     	2.getInitialState   设置组件默认的state 
     	3.componentWillMount  在jsx被渲染到页面之前被调用
     	4.render   渲染函数是react中默认的函数
     	5.componentDidMount   jsx被渲染到页面后被调用

8.  react 性能优化的方案 

    你所不知道的render

    更新阶段的生命周期

    shouldComponentUpdate

    key

    [链接](https://segmentfault.com/a/1190000007811296)

9.  react 如何校验 props 和 context 

    React.PropTypes

    context？？？

10. 简述一下 flux 的思想

    [Flux的核心思想就是数据和逻辑永远单向流动](https://www.jianshu.com/p/79f414053384)。数据从action到dispatcher，再到store,最终到view的路线是单向不可逆的。

react 专场 2

1.  [react 父子组件通信方式有哪些](https://www.jianshu.com/p/cf0fcc2c53fc) ？

    父子组件：props

    子父组件通讯：props，ref

    跨级组件通信：context

2.  react ES6 创建组件中如何初始化定义 state 和 props  context

    state的初始化，通过构造函数

    ```js
    //在构造函数中对状态赋初始值
        constructor(props){
            super(props);//第一步，这是必须的
            //不能调用state
            this.state = {//第二步，赋初始值
                time:0,
                on:false,
                log:[] //数组
            };
        }
    
    ```

    props的初始化

    ```js
    class Button extends React.Component{
    //静态属性，给属性赋默认值
    static defaultProps = {
        onClick : null,
        className : '',
        text : '默认'
    };
    
    render(){
        return <button className={`Button ${this.props.className}`} onClick={this.props.onClick}>{this.props.text}</button>;
    }
    
    ```

    context？？

3.  [react 路由中 如何 传递参数 如何在组件内部获取参数](https://blog.csdn.net/qtfying/article/details/77939171)  

    props.params

    query

    state

    onclick

4.  react 路由中 组件可以在props 获取三个属性 分别是什么? 有什么作用

    history 

    location

    match

5.  react 路由中 如何切换路由模式,什么情况下需要设置 basename 属性 

    https://www.jb51.net/article/119511.htm
    https://blog.csdn.net/Allence_z/article/details/80949436

6.  react 里面架构管理 redux 的原理 以及分层 

    http://www.alloyteam.com/2015/09/react-redux/

    （解答：问这个问题说明你还没有搞清redux的工作原理。我们拿银行来做类比，首先银行会有有一个专门的地方存放，而这个存钱的地方就是redux的store。我们现实生活中要存钱或者取钱，肯定不能让你直接去存钱的地方拿钱吧！你得提交申请，银行审核通过之后，银行柜台才能帮你存钱或者取钱吧。这里对应redux就是，你想修改或者读取store的数据，你是不能直接操作store的，你得发起一个申请，这个申请就是action。发出申请之后，得有人来审核，那这个人就是reducer。他会判断你要做类型的事情，比如存钱还是取钱，然后再帮你去store进行相应的操作。知道原理之后，我们来理一下这个两个东西是干嘛的。ADD_TODO在这里就相当于业务类型，为什么要暴露出来，你的addTodo这个申请对应的业务类型就是ADD_TODO，你不暴露给reducer，reducer怎么判断要进行什么操作？）https://segmentfault.com/q/1010000011378862

7.  react redux 里面 action 和 reducers 各有什么特点 和作用 

     Reducer 一般为简单的处理函数，通过传入旧的 state 和指示操作的 action 来更新 state

    action 主要用来传递操作 State 的信息

8.  react-redux 有2种组件划分 ,分别是什么，各有什么作用

    显示组件与容器组件

    显示组件：显示组件是只能有显示内容的东西。

    容器组件：容器组件其实主要负责的是数据的获取和服务器的交互。

    一般显示组件只负责展示内容，一般容器组件主要负责数据处理，服务器交互之类的，也会负责一些显示内容。

9.  [react-redux 里面如何实现异步操作？](https://segmentfault.com/a/1190000016012907?utm_source=tag-newest) 

    

10. react架构管理redux/react-redux 有什么缺点吗?

    优势： React 和 Redux 的最大优势在于它们相对简单和专注，可以轻松掌握概念，并了解单向数据体系结构的好处，简化大量的用户界面应用程序。

    缺点：  React 和 Redux 最大的弱点不是它们是什么，而是它们不是什么。要构建一个功能丰富的 Web 应用程序，你需要许多功能，一旦脱离 React 和 Redux 和其他一些库的核心，你将发现一个非常分散的社区，拥有无数的解决方案和模式，不容易整合在一起。

11. [react 和 vue 对比,如何选择](https://blog.csdn.net/yzh_2017/article/details/54909166)

    如果你喜欢用（或希望能够用）模板搭建应用或简单和“能用就行”的东西或应用需要尽可能的小和快，请使用Vue。
    如果你计划构建一个大型应用程序或想要一个同时适用于Web端和原生App的框架或想要最大的生态圈，请使用React。
    如果你已经对其中一个用得满意了，就没有必要换了

12. react 如何封装组件 

    目前有两种常用的方法定义组件：函数式组件、类组件。

    通过props，分发（this.props.children----swiper组件）

    https://www.imooc.com/article/40697

13. 为什么虚拟DOM会提升性能

    因为虚拟DOM以 js结构的形式存在，计算性能会比较好，而且由于减少了实际DOM操作次数，性能会有很大提示。

node 专场 1 

1.  node 开发 中你用过哪些常用的node模块，分别是哪些?

    http模块，https模块，url，fs，querystring（模块提供用于解析和格式化 URL 查询字符串的实用工具），加密。

2.  node 开发中 如何实现 模块化开发  （什么是模块化开发 怎么实现模块化开发） require exports defined  

    node开发中遵循commonJs规范，将模块定义，模块导出，模块导入。

3.  node 开发 返回的数据的文档类型格式有哪些 5条 （content-type）

    json，txt，jsonp，xml，html，jpg

4.  npm 安装插件 package  如何 安装开发依赖 项目依赖 全局依赖 underscore  yarn 如何安装插件  

    开发依赖npm i ** -D,

    项目依赖npm i **  -S,

    全局依赖npm i **  -g, 

    yarn add global ---, yarn add

5.  node 文件读取 这个 模块  读文件 写文件  创建文件  删除文件  怎么实现 

    fs.readFile fs.writeFile fs.createFile fs.unlink

6.  mongodb 和 mysql 数据库的区别 

    MySQL是关系型数据库。

    Mongodb是非关系型数据库(nosql ),属于文档型数据库。

7.  分别写出mongodb 和 mysql 数据库的增删改查    数据表 为 user 

    mongodb：db.user.find() 	db.user.insert() 	db.user.remove() 	db.user.update()
    mysql: select * from user

8.  node 什么是 socket ，它有什么作用 ? 

    node里面的socket、实现不同客服端之间的通信，通过服务器与客户端之间的通信实现。

9.  什么是长连接 , 你知道的有哪些 实现 长连接的 方式  sse socket （ajax是短连接，是三次握手）

    在HTTP/1.0中默认使用短连接。也就是说，客户端和服务器每进行一次HTTP操作，就建立一次连接，任务结束就中断连接。当客户端浏览器访问的某个HTML或其他类型的Web页中包含有其他的Web资源（如JavaScript文件、图像文件、CSS文件等），每遇到这样一个Web资源，浏览器就会重新建立一个HTTP会话。

    而从HTTP/1.1起，默认使用长连接，用以保持连接特性。使用长连接的HTTP协议，会在响应头加入这行代码：

    ```
    Connection:keep-alive
    ```

    在使用长连接的情况下，当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，客户端再次访问这个服务器时，会继续使用这一条已经建立的连接。Keep-Alive不会永久保持连接，它有一个保持时间，可以在不同的服务器软件（如Apache）中设定这个时间。实现长连接需要客户端和服务端都支持长连接。

    HTTP协议的长连接和短连接，实质上是TCP协议的长连接和短连接。

10.  说一下[加密方式](https://blog.csdn.net/mirage003/article/details/80724723)有哪些 谈一下基于node 加密模块 

     base64	sha1 md5

     node使用require('crypto')调用加密模块。

11.  node + express ejs 后端模板引擎 有哪些特点  

     涉及到混合开发

12.  express  req.query  req.body  req.params  分别是什么意思?

     https://www.jianshu.com/p/c2cd8ee61722

     req.params：取带冒号的参数

     req.body：可以肯定的一点是req.body一定是post请求，express里依赖的中间件必须有bodyParser，不然req.body是没有的。

     req.query：说明req.query不一定是get

原生 专场 1
1. 什么是ajax, [简述一下 ajax 请求数据的过程](https://www.cnblogs.com/xiaozhijing/p/7920851.html) 

    AJAX即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。
    通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

    ```
    get 请求
    1) 创建一个XMLHttpRequest对象
    2) 调用该对象的open方法
    3) 如果是get请求，设置回调函数onreadystatechange = callback
    4) Send
    
    如果是post 请求
    5) 创建一个XMLHttpRequest对象
    6) 调用该对象的open方法
    7) 调用setRequestHeader(“Content-Type”, “application/x-www-form-urlencoded”);
    8) 设置回调函数onreadystatechange = callback
    9) Send
    ```

2. 简述 this 的 四种指向 问题 

    a.如果是一般函数,this指向全局对象window;
    b.在严格模式下"use strict",为undefined.
    c.对象的方法里调用,this指向调用该方法的对象.
    d.构造函数里的this,指向创建出来的实例.

3. jquery 的优点和缺点  

4. 跨域如何产生 如何解决跨域 

5. 什么是闭包 项目如何使用闭包 闭包有什么优缺点 

6. 谈谈你对面向对象的理解  面向对象的特点   

7. 如何深入理解原型链

8. setInterval/setTimeout 传参数 的四种不同写法  

9. 如何区分  宿主对象  内置对象  本地对象  分别有哪些? 

10. url  https://www.aliyun.com/node/day?id=1234&price=100#level1   
    协议  域名  search  query path pathname host hostname  hash

11. Query 中，$.data() 和 $(“#aa”).data() 各自是什么作用，有什么区别？

12. jQuery 中 ， $.fn ($ = jQuery) 和 $.prototype  三种的区别  $  和 jQuery 的区别 

13. 简述一下 你对  TCP三次握手 的理解 

14. 如何判断你当前手机浏览器的厂商 userAgent

15. $.fn.extends    $.extends   两者的区别 

混合开发+ ES6 专场 

1. 简述一下你知道的有哪些ES6的新特性

2. 说一下什么是块级作用域 , 它有什么作用

3. 谈谈箭头函数 有什么特点  ()=>{}

4. class 类 中 super关键字  super 当函数时表示什么?super当对象时表示什么?

5. ES6 中你是怎么使用 promise 的 ？ 

6. 严格模式 怎么声明  严格模式 有什么 特点 ? （3-4条）

7. 混合开发的原理(cordova DCloud 微信JSSDK)

8. 混合开发的优缺点 

9. 微信小程序  你知道的有哪些 API  和哪些常用的 组件  (SDK JDK)

10. 变量提升如何产生?

11. 你在实际开发中如何和IOS/Android 程序员进行交互的。

12. 微信小程序开发 中   关于 page的生命周期钩子函数 有哪些?

13. 微信小程序 如何设置 https 请求 , wx.request 可以使用 POST 请求吗？

14. 微信小程序 你经常使用哪些指令 wx:if wx:for hidden 

15. 微信小程序 绑定事件  bindtap 和 catch 的区别   



面试专场 

1.  html5 新特性  

    HTML5 中的一些有趣的新特性：

    -   用于绘画的 canvas 元素
    -   用于媒介回放的 video 和 audio 元素
    -   对本地离线存储的更好的支持
    -   新的特殊内容元素，比如 article、footer、header、nav、section
    -   新的表单控件，比如 calendar、date、time、email、url、search

2.  本地存储指的是什么? localStorage&sessionStorage 的区别?什么是离线存储 

    离线存储 可以保证在没有网络的情况下访问一部分资源

3.  前端性能优化的方法有哪些? 6条 

    https://www.cnblogs.com/mhxy13867806343/p/8446218.html

    css js 压缩

    尽量使用图片服务器，

    js加载到后面

    使用缓存

    减少前端http请求

4.  你知道浏览器兼容的bug有哪些，说出对应兼容bug的解决方式 3 条 

    https://jingyan.baidu.com/article/d169e1864f9c53436611d8eb.html

    https://blog.csdn.net/weixin_38536027/article/details/79375411

5.  如何判断你当初浏览器的类型和提供商?  DOM和BOM的区别  nagivator.userAgent

6.  DOM和DOM2事件写法的区别?

    onclick

    addeventlistner？？

    dom0级后面绑定的事件会覆盖前面绑定的事件，点击的时候会执行新绑定的

    dom2级不会覆盖前面绑定的事件，点击的时候所有绑定的事件会依次执行一遍

7.  如何使元素垂直水平居中? 4种 

    <!-- 

    ​    垂直水平居中

    ​    \1.  

    ​        position: relative; 父 

    ​        position: absolute;

    ​        width:100px;

    ​        height:100px;

    ​        top:0;

    ​        left:0;

    ​        right:0;

    ​        bottom:0;

    ​        margin: auto;

    

    ​    \2. margin 负值

    ​        position: relative; 父 

    ​        position: absolute;

    ​        width:100px;

    ​        height:100px;

    ​        top:50%;

    ​        left:50%;

    ​        margin: -50%;

    

    ​    \3.  tranlsate 

    ​        position: relative; 父 

    ​        position: absolute;

    ​        width:100px;

    ​        height:100px;

    ​        top:50%;

    ​        left:50%;

    ​        transform: translate(-50%,-50%);

    

    ​     4.table-cell  父

    

    ​     \5. 父   

    ​        display: flex;

    ​        justify-content: center;

    ​        align-items: center;

    ​        

    ​    \6. 父

    ​        display: flex;

    ​        justify-content: center;

    ​        子

    ​        display: flex;

    ​        align-self:center

     -->

8.  webpack和gulp的区别？

    gulp强调的是前端开发的工作流程。实现项目工程自动化。自动复制打包（两个js合并到一起）。

    webpack是一个前端模块化方案，更侧重模块打包，

    https://www.cnblogs.com/lovesong/p/6413546.html

9.  简述你最近一个项目的开发流程

    https://www.cnblogs.com/hzg8754/p/9641398.html 

    项目确定，讨论需求（bug，验证码登录注册，抽奖功能--概率，实时推送，），确定Ui，讨论框架（vue或者react），后台开发接口，静态页面开发，接口联调（ajax请求），测试（本地，线上），上线。

10.  说一下你在公司中 项目上线的步骤 

     推到git（svn）服务器分支，发邮件运维测试自取，（加入没上线过）

随便问问 专场 

1.  你觉得的HTTP的状态码有哪些?仔细说明

    https://www.cnblogs.com/yunshangwuyou/p/9578568.html

    https://blog.csdn.net/fatong3/article/details/80350731

2.  ajax 异步请求数据的步骤？

    https://www.cnblogs.com/chenzechuang/p/6637794.html

    2 . ajax异步请求数据的步骤？

    1.创建XMLHttpRequest

    2.连接服务器 get/post

    3.向服务器端发送请求

    4.接受服务器的返回

    

    1 创建XMLHttpRequest 对象 ，也就是创建一个异步调用的对象

    2 创建一个新的HTTP请求， 并指定该HTTP请求的方法，URL及验证信息

    3  设置响应HTTP请求状态变化的函数

    4  发送HTTP请求

    5  获取异步调用返回的数据

    6  使用js和dom实现局部刷新

3.  你项目中如何处理跨域请求?（JSONP 反向代理 postMessage CROS）

    https://www.cnblogs.com/wendy-home-5678/p/6819188.html

    JSONP：利用script里的src属性（src不会受到同源策略影响）

    反向代理：https://www.cnblogs.com/renjing/p/6394725.html，proxy

4.  Jsonp的原理,解释一下JSONP为什么不是真正的ajax

    https://www.jianshu.com/p/93ebb6982481

5.  什么是事件委托? 列举使用事件委托的地方 

    事件的冒泡

    给一个不存在的元素（未来元素）添加事件时

    https://blog.csdn.net/cz_sky/article/details/75884502

6.  你如何在jquery  插件的基础上封装新的插件 (\$.extend \$.fn.extend ) ($ 和 ​\$.fn 的区别 )

    静态对象\实例对象

7.  使用版本控制工具git/svn 产生冲突 你如何解、

    https://blog.csdn.net/qq_31649521/article/details/81181868

    1.  把本地的代码修改成与远程的一样时提交
    2.  只推送没拉取（故事）

8.  说一下你最近项目开发的技术亮点 

    使用了elementUI，使用了懒加载，

9.  说一下你的前端成长经历,你是如何一步步成为前端大牛的?

    经常逛一些技术论坛，实时关注当前的最新技术框架，

10.  如何看待当前前端发展的趋势,和未来技术走向?

     未来的前端覆盖面会越来越广泛，技术复杂度越来越深，ts与后台很像

11.  你知道哪些设计模式 

     mvc mvvm mvp 发布订阅 工厂模式

     （1）单例模式

     定义：保证一个类仅有一个实例，并提供一个访问它的全局访问点。

     实现方法：先判断实例存在与否，如果存在则直接返回，如果不存在就创建了再返回，这就确保了一个类只有一个实例对象。

     适用场景：一个单一对象。比如：弹窗，无论点击多少次，弹窗只应该被创建一次。

     （2）发布/订阅模式

     定义：又叫观察者模式,它定义对象间的一种一对多的依赖关系,当一个对象的状态发生改变时,所有依赖于它的对象都将得到通知。

     场景：订阅感兴趣的专栏和公众号。

     （3）策略模式

     定义：将一个个算法（解决方案）封装在一个个策略类中。

     优点：

     策略模式可以避免代码中的多重判断条件。

     策略模式很好的体现了开放-封闭原则，将一个个算法（解决方案）封装在一个个策略类中。便于切换，理解，扩展。

     策略中的各种算法可以重复利用在系统的各个地方，避免复制粘贴。

     策略模式在程序中或多或少的增加了策略类。但比堆砌在业务逻辑中要清晰明了。

     违反最少知识原则，必须要了解各种策略类，才能更好的在业务中应用。

     应用场景：根据不同的员工绩效计算不同的奖金；表单验证中的多种校验规则。

     （4）代理模式

     定义：为一个对象提供一个代用品或占位符，以便控制对它的访问。

     应用场景：图片懒加载（先通过一张loading图占位，然后通过异步的方式加载图片，等图片加载好了再把完成的图片加载到img标签里面。）

     （5）中介者模式

     定义：通过一个中介者对象，其他所有相关对象都通过该中介者对象来通信，而不是互相引用，当其中的一个对象发生改变时，只要通知中介者对象就可以。可以解除对象与对象之间的紧耦合关系。

     应用场景： 例如购物车需求，存在商品选择表单、颜色选择表单、购买数量表单等等，都会触发change事件，那么可以通过中介者来转发处理这些事件，实现各个事件间的解耦，仅仅维护中介者对象即可。

     （6）装饰者模式

     定义：在不改变对象自身的基础上，在程序运行期间给对象动态的添加方法。

     应用场景： 有方法维持不变，在原有方法上再挂载其他方法来满足现有需求；函数的解耦，将函数拆分成多个可复用的函数，再将拆分出来的函数挂载到某个函数上，实现相同的效果但增强了复用性。







补充：

1.  w3c规范：万维网联盟（外语缩写：W3C）标准不是某一个标准，而是一系列标准的集合。网页主要由三部分组成：结构（Structure）、表现（Presentation）和行为（Behavior）。比如！声明文档类型。标签闭合，代码缩进，语义化标签。
