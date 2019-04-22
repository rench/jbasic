## 知识点
### HTML&CSS

对Web标准的理解、浏览器内核差异、兼容性、hack、CSS基本功：布局、盒子模型、选择器优先级及使用、HTML5、CSS3、移动端适应。

### JavaScript

数据类型、面向对象、继承、闭包、插件、作用域、跨域、原型链、模块化、自定义事件、内存泄漏、事件机制、异步装载回调、模板引擎、Nodejs、JSON、ajax。

https://github.com/FEGuideTeam/FEGuide/tree/master/javascript%E9%97%AE%E9%A2%98

- 说几条写 JavaScript 的基本规范
    
    - 代码缩进，建议使用“四个空格”缩进
    - 代码段使用花括号{}包裹
    - 语句结束使用分号;
    - 变量和函数在使用前进行声明
    - 以大写字母开头命名构造函数，全大写命名常量
    - 规范定义 JSON 对象，补全双引号
    - 用{}和[]声明对象和数组

- DOM 元素 e 的 e.getAttribute(propName)和 e.propName 有什么区别和联系

    - e.getAttribute()，是标准 DOM 操作文档元素属性的方法，具有通用性可在任意文档上使用，返回元素在源文件中设置的属性
    - e.propName 通常是在 HTML 文档中访问特定元素的特性，浏览器解析元素后生成对应对象（如 a 标签生成 HTMLAnchorElement），这些对象的特性会根据特定规则结合属性设置得到，对于没有对应特性的属性，只能使用 getAttribute 进行访问
    - e.getAttribute()返回值是源文件中设置的值，类型是字符串或者 null（有的实现返回""）
    - e.propName 返回值可能是字符串、布尔值、对象、undefined 等
    - 大部分 attribute 与 property 是一一对应关系，修改其中一个会影响另一个，如 id，title 等属性
    - 一些布尔属性`<input hidden/>`的检测设置需要 hasAttribute 和 removeAttribute 来完成，或者设置对应 property
    - 像`<a href="../index.html">link</a>`中 href 属性，转换成 property 的时候需要通过转换得到完整 URL
    - 一些 attribute 和 property 不是一一对应如：form 控件中`<input value="hello"/>`对应的是 defaultValue，修改或设置 value property 修改的是控件当前值，setAttribute 修改 value 属性不会改变 value property

- offsetWidth/offsetHeight,clientWidth/clientHeight 与 scrollWidth/scrollHeight 的区别

    - offsetWidth/offsetHeight 返回值包含 content + padding + border，效果与 e.getBoundingClientRect()相同
    - clientWidth/clientHeight 返回值只包含 content + padding，如果有滚动条，也不包含滚动条
    - scrollWidth/scrollHeight 返回值包含 content + padding + 溢出内容的尺寸
    
- 描述浏览器的渲染过程，DOM 树和渲染树的区别？

    浏览器的渲染过程
    
    - 解析 HTML 构建 DOM(DOM 树)，并行请求 css/image/js
    - CSS 文件下载完成，开始构建 CSSOM(CSS 树)
    - CSSOM 构建结束后，和 DOM 一起生成 Render Tree(渲染树)
    - 布局(Layout)：计算出每个节点在屏幕中的位置
    - 显示(Painting)：通过显卡把页面画到屏幕上
    
    DOM 树 和 渲染树 的区别：
    
    - DOM 树与 HTML 标签一一对应，包括 head 和隐藏元素
    - 渲染树不包括 head 和隐藏元素，大段文本的每一个行都是独立节点，每一个节点都有对应的 css 属性

- script 的位置是否会影响首屏显示时间？
    - 在解析 HTML 生成 DOM 过程中，js 文件的下载是并行的，不需要 DOM 处理到 script 节点。因此，script 的位置不影响首屏显示的开始时间。
    - 浏览器解析 HTML 是自上而下的线性过程，script 作为 HTML 的一部分同样遵循这个原则
    - 因此，script 会延迟 DomContentLoad，只显示其上部分首屏内容，从而影响首屏显示的完成时间

- Javascript 如何实现继承？
    - 构造函数绑定：使用 call 或 apply 方法，将父对象的构造函数绑定在子对象上
    ```
    function Cat(name,color){
     　Animal.apply(this, arguments);
     　this.name = name;
     　this.color = color;
    }
    ```
    - 实例继承：将子对象的 prototype 指向父对象的一个实例
    ```
    Cat.prototype = new Animal();
    Cat.prototype.constructor = Cat;
    ```
    - 拷贝继承：如果把父对象的所有属性和方法，拷贝进子对象
    ```
    function extend(Child, Parent) {
    　　　var p = Parent.prototype;
    　　　var c = Child.prototype;
    　　　for (var i in p) {
    　　　   c[i] = p[i];
    　　　}
    　　　c.uber = p;
    }
    ```
    - 原型继承：将子对象的 prototype 指向父对象的 prototype
    ```
    function extend(Child, Parent) {
        var F = function(){};
        　F.prototype = Parent.prototype;
        　Child.prototype = new F();
        　Child.prototype.constructor = Child;
        　Child.uber = Parent.prototype;
    }
    ```
    - ES6 语法糖 extends：class ColorPoint extends Point {}
    ```
    class ColorPoint extends Point {
        constructor(x, y, color) {
            super(x, y); // 调用父类的constructor(x, y)
            this.color = color;
        }
        toString() {
            return this.color + ' ' + super.toString(); // 调用父类的toString()
        }
    }
    ```

- 事件冒泡、事件捕获

https://blog.csdn.net/qq_34626003/article/details/71079449

- 如何派发事件(dispatchEvent)？（如何进行事件广播？）
    - W3C: 使用 dispatchEvent 方法
    - IE: 使用 fireEvent 方法
    ```
    var fireEvent = function(element, event){
        if (document.createEventObject){
            var mockEvent = document.createEventObject();
            return element.fireEvent('on' + event, mockEvent)
        }else{
            var mockEvent = document.createEvent('HTMLEvents');
            mockEvent.initEvent(event, true, true);
            return !element.dispatchEvent(mockEvent);
        }
    }
    ```
- 什么是函数节流？介绍一下应用场景和原理？
函数节流(throttle)是指阻止一个函数在很短时间间隔内连续调用。 只有当上一次函数执行后达到规定的时间间隔，才能进行下一次调用。 但要保证一个累计最小调用间隔（否则拖拽类的节流都将无连续效果）
函数节流用于 onresize, onscroll 等短时间内会多次触发的事件
函数节流的原理：使用定时器做时间节流。 当触发一个事件时，先用 setTimout 让这个事件延迟一小段时间再执行。 如果在这个时间间隔内又触发了事件，就 clearTimeout 原来的定时器， 再 setTimeout 一个新的定时器重复以上流程。

### 框架
#### React

- React 中 keys 的作用是什么？
    
    Keys 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。

    在开发过程中，我们需要保证某个元素的 key 在其同级元素中具有唯一性。在 React Diff 算法中 React 会借助元素的 Key 值来判断该元素是新近创建的还是被移动而来的元素，从而减少不必要的元素重渲染。此外，React 还需要借助 Key 值来判断元素与本地状态的关联关系，因此我们绝不可忽视转换函数中 Key 的重要性。
    
- 调用 setState 之后发生了什么？

    在代码中调用 setState 函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程（Reconciliation）。经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个 UI 界面。在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。
    
- react 生命周期函数
    - 初始化阶段：
        - getDefaultProps:获取实例的默认属性
        - getInitialState:获取每个实例的初始化状态
        - componentWillMount：组件即将被装载、渲染到页面上
        - render:组件在这里生成虚拟的 DOM 节点
        - componentDidMount:组件真正在被装载之后
    - 运行中状态：
        - componentWillReceiveProps:组件将要接收到属性的时候调用
        - shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回 false，接收数据后不更新，阻止 render 调用，后面的函数不会被继续执行了）
        - componentWillUpdate:组件即将更新不能修改属性和状态
        - render:组件重新描绘
        - componentDidUpdate:组件已经更新
    - 销毁阶段：
        - componentWillUnmount:组件即将销毁
- 为什么虚拟 dom 会提高性能?

    虚拟 dom 相当于在 js 和真实 dom 中间加了一个缓存，利用 dom diff 算法避免了没有必要的 dom 操作，从而提高性能。
    
    用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异把 2 所记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了。
    
- 如何理解虚拟DOM?           

    https://www.zhihu.com/question/29504639?sort=created

- react diff 原理
    - 把树形结构按照层级分解，只比较同级元素。
    - 给列表结构的每个单元添加唯一的 key 属性，方便比较。
    - React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
    - 合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
    - 选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。
    - React 的 diff 算法 https://segmentfault.com/a/1190000000606216

- 应该在 React 组件的何处发起 Ajax 请求

    在 React 组件中，应该在 componentDidMount 中发起网络请求。这个方法会在组件第一次“挂载”(被添加到 DOM)时执行，在组件的生命周期中仅会执行一次。更重要的是，你不能保证在组件挂载之前 Ajax 请求已经完成，如果是这样，也就意味着你将尝试在一个未挂载的组件上调用 setState，这将不起作用。在 componentDidMount 中发起网络请求将保证这有一个组件可以更新了。

- createElement 和 cloneElement 有什么区别？
    - React.createElement():JSX 语法就是用 React.createElement()来构建 React 元素的。它接受三个参数，第一个参数可以是一个标签名。如 div、span，或者 React 组件。第二个参数为传入的属性。第三个以及之后的参数，皆作为组件的子组件。
    ```
    React.createElement(
        type,
        [props],
        [...children]
    )
    ```
    - React.cloneElement()与 React.createElement()相似，不同的是它传入的第一个参数是一个 React 元素，而不是标签名或组件。新添加的属性会并入原有的属性，传入到返回的新元素中，而就的子元素奖杯替换。
    ```
    React.cloneElement(
      element,
      [props],
      [...children]
    )
    ```
- React 中有三种构建组件的方式
    
    React.createClass()、ES6 class 和无状态函数。

- react 组件的划分业务组件技术组件？
    - 根据组件的职责通常把组件分为 UI 组件和容器组件。
    - UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。
    - 两者通过 React-Redux 提供 connect 方法联系起来。
    
- 简述 flux 思想
     
    Flux 的最大特点，就是数据的"单向流动"。
    - 用户访问 View
    - View 发出用户的 Action
    - Dispatcher 收到 Action，要求 Store 进行相应的更新
    - Store 更新后，发出一个"change"事件
    - View 收到"change"事件后，更新页面

- React 项目用过什么脚手架

    - creat-react-app
    - Yeoman 等

- 了解 redux 么，说一下redux吧
    
    - redux 是一个应用数据流框架，主要是解决了组件间状态共享的问题，原理是集中式管理，主要有三个核心方法，action，store，reducer，工作流程是 view 调用 store 的 dispatch 接收 action 传入 store，reducer 进行 state 操作，view 通过 store 提供的 getState 获取最新的数据，flux 也是用来进行数据操作的，有四个组成部分 action，dispatch，view，store，工作流程是 view 发出一个 action，派发器接收 action，让 store 进行数据更新，更新完成以后 store 发出 change，view 接受 change 更新视图。Redux 和 Flux 很像。主要区别在于 Flux 有多个可以改变应用状态的 store，在 Flux 中 dispatcher 被用来传递数据到注册的回调事件，但是在 redux 中只能定义一个可更新状态的 store，redux 把 store 和 Dispatcher 合并,结构更加简单清晰
    - 新增 state,对状态的管理更加明确，通过 redux，流程更加规范了，减少手动编码量，提高了编码效率，同时缺点时当数据更新时有时候组件不需要，但是也要重新绘制，有些影响效率。一般情况下，我们在构建多交互，多数据流的复杂项目应用时才会使用它们

- redux 有什么缺点

    - 一个组件所需要的数据，必须由父组件传过来，而不能像 flux 中直接从 store 取。
    - 当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新 render，可能会有效率影响，或者需要写复杂的 shouldComponentUpdate 进行判断。
    
#### vue
https://github.com/FEGuideTeam/FEGuide/blob/master/框架/vue.md
- 什么是 mvvm？
    
    MVVM 是 Model-View-ViewModel 的缩写。mvvm 是一种设计思想。Model 层代表数据模型，也可以在 Model 中定义数据修改和操作的业务逻辑；View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来，ViewModel 是一个同步 View 和 Model 的对象。

    在 MVVM 架构下，View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向的， 因此 View 数据的变化会同步到 Model 中，而 Model 数据的变化也会立即反应到 View 上。
    
    ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作 DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

- mvvm 和 mvc 区别？

    mvc 和 mvvm 其实区别并不大。都是一种设计思想。主要就是 mvc 中 Controller 演变成 mvvm 中的 viewModel。mvvm 主要解决了 mvc 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。和当 Model 频繁发生变化，开发者需要主动更新到 View 。
    
- vue 的优点是什么？
    
    - 低耦合。视图（View）可以独立于 Model 变化和修改，一个 ViewModel 可以绑定到不同的"View"上，当 View 变化的时候 Model 可以不变，当 Model 变化的时候 View 也可以不变。
    - 可重用性。你可以把一些视图逻辑放在一个 ViewModel 里面，让很多 view 重用这段视图逻辑。
    - 独立开发。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计，使用 Expression Blend 可以很容易设计界面并生成 xml 代码。
    - 可测试。界面素来是比较难于测试的，而现在测试可以针对 ViewModel 来写。
    
- 请详细说下你对 vue 生命周期的理解？
    总共分为 8 个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

    - 创建前/后： 在 beforeCreate 阶段，vue 实例的挂载元素 el 还没有。
    
    - 载入前/后：在 beforeMount 阶段，vue 实例的$el 和 data 都初始化了，但还是挂载之前为虚拟的 dom 节点，data.message 还未替换。在 mounted 阶段，vue 实例挂载完成，data.message 成功渲染。
    
    - 更新前/后：当 data 变化时，会触发 beforeUpdate 和 updated 方法。
    
    - 销毁前/后：在执行 destroy 方法后，对 data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 dom 的绑定，但是 dom 结构依然存在
    
- vuex 是什么？怎么使用？哪种功能场景使用它？
    
    vue 框架中状态管理。在 main.js 引入 store，注入。新建了一个目录 store，….. export 。场景有：单页应用中，组件之间的状态。音乐播放、登录状态、加入购物车

- vue-router 有哪几种导航钩子?
    
    - 全局导航钩子
        - router.beforeEach(to, from, next),
        - router.beforeResolve(to, from, next),
        - router.afterEach(to, from ,next)
    - 组件内钩子
        - beforeRouteEnter,
        - beforeRouteUpdate,
        - beforeRouteLeave
    - 单独路由独享组件
        - beforeEnter
- 说出至少 4 种 vue 当中的指令和它的用法
    
    - v-if(判断是否隐藏)
    - v-for(把数据遍历出来)
    - v-bind(绑定属性)
    - v-model(实现双向绑定)

- vue 的双向绑定的原理是什么

    vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过 Object.defineProperty()来劫持各个属性的 setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。
    
    具体步骤： 第一步：需要 observe 的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter 和 getter 这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化
    
    第二步：compile 解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
    
    第三步：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁，主要做的事情是:
        - 在自身实例化时往属性订阅器(dep)里面添加自己
        - 自身必须有一个 update()方法
        - 待属性变动 dep.notice()通知时，能调用自身的 update() 方法，并触发 Compile 中绑定的回调，则功成身退。
        
    第四步：MVVM 作为数据绑定的入口，整合 Observer、Compile 和 Watcher 三者，通过 Observer 来监听自己的 model 数据变化，通过 Compile 来解析编译模板指令，最终利用 Watcher 搭起 Observer 和 Compile 之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据 model 变更的双向绑定效果。
    
- vuex 有哪几种属性
    有 5 种，分别是 state、getter、mutation、action、module
- vuex 的 store 特性是什么
    - vuex 就是一个仓库，仓库里放了很多对象。其中 state 就是数据源存放地，对应于一般 vue 对象里面的 data
    - state 里面存放的数据是响应式的，vue 组件从 store 读取数据，若是 store 中的数据发生改变，依赖这相数据的组件也会发生更新
    - 它通过 mapState 把全局的 state 和 getters 映射到当前组件的 computed 计算属性
- vuex 的 getter 特性是什么
    - getter 可以对 state 进行计算操作，它就是 store 的计算属性
    - 虽然在组件内也可以做计算属性，但是 getters 可以在多给件之间复用
    - 如果一个状态只在一个组件内使用，是可以不用 getters

- vuex 的 mutation 特性是什么
    - action 类似于 muation, 不同在于：action 提交的是 mutation,而不是直接变更状态
    - action 可以包含任意异步操作

- vue 中 ajax 请求代码应该写在组件的 methods 中还是 vuex 的 action 中
    - 如果请求来的数据不是要被其他组件公用，仅仅在请求的组件内使用，就不需要放入 vuex 的 state 里
    - 如果被其他地方复用，请将请求放入 action 里，方便复用，并包装成 promise 返回

- 不用 vuex 会带来什么问题
    - 可维护性会下降，你要修改数据，你得维护 3 个地方
    - 可读性下降，因为一个组件里的数据，你根本就看不出来是从哪里来的
    - 增加耦合，大量的上传派发，会让耦合性大大的增加，本来 Vue 用 Component 就是为了减少耦合，现在这么用，和组件化的初衷相背

- vuex 原理
    - vuex 仅仅是作为 vue 的一个插件而存在，不像 Redux,MobX 等库可以应用于所有框架，vuex 只能使用在 vue 上，很大的程度是因为其高度依赖于 vue 的 computed 依赖检测系统以及其插件系统，
    - vuex 整体思想诞生于 flux,可其的实现方式完完全全的使用了 vue 自身的响应式设计，依赖监听、依赖收集都属于 vue 对对象 Property set get 方法的代理劫持。最后一句话结束 vuex 工作原理，vuex 中的 store 本质就是没有 template 的隐藏着的 vue 组件；

- vuex 原理 
    https://tech.meituan.com/2017/04/27/vuex-code-analysis.html

- axios
    
    axios 是请求后台资源的模块。 npm i axios -S

    如果发送的是跨域请求，需在配置文件中 config/index.js 进行配置

### 其他

HTTP、安全、正则、优化、重构、响应式、移动端、团队协作、可维护、SEO、UED、架构、职业生涯