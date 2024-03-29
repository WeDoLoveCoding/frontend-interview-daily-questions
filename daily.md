# 什么是 let 的临时性死区?

let 声明的变量在被声明之前不能被访问，这被称为 "临时性死区"（Temporal Dead Zone，缩写为 TDZ）。

在 let 声明之前，对该变量的任何引用都会导致 ReferenceError 错误。临时性死区从变量被声明开始，直到变量被实际赋值为止。

这个行为的原因是因为 let 声明是块级作用域，而不是函数作用域。在代码块内，let 声明的变量只能在声明之后访问。在 TDZ 内，该变量被认为是已经声明但未定义的，因此在访问它之前会抛出错误。

# async/await 和 Promise 有什么关系?

async/await 是一种基于 Promise 的异步编程模式，是 ECMAScript 2017（ES8）中的新增语法糖。它是用于处理异步操作的一种更加直观和易用的方法，可以使得异步代码的编写和理解更加简单和直接。

在使用 async/await 时，可以使用关键字 async 来声明一个异步函数，该函数内部可以使用 await 关键字来等待异步操作的结果。当使用 await 等待一个 Promise 对象时，该操作会自动挂起当前的异步函数，直到该 Promise 对象的状态变为 resolved（已完成）或 rejected（已拒绝）。

实际上，async/await 是建立在 Promise 之上的语法糖，它可以使得使用 Promise 的异步代码更加简洁和易读。使用 async/await 可以避免一些 Promise 链式调用的嵌套，提高代码可读性和可维护性。

# HTTP 协议的优点和缺点

HTTP 是超文本传输协议，它定义了客户端和服务器之间交换报文的格式和方式，默认使用 80 端口。它使用 TCP 作为传输层协议，保证数据传输的可靠性

HTTP 协议具有以下优点：

- 支持客户端/服务器模式

- 简单快速：客户向服务器请求服务时，只需传达请求方法和路径。由于 HTTP 协议简单，使得 HTTP 服务器的程序规模小，因而通信速度很快

- 无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接，采用这种方式可以节省传输时间

- 无状态：HTTP 协议是无状态协议，这里的状态是指通信过程的上下文信息。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能会导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就比较快

- 灵活：HTTP 允许传输任意类型的数据对象。正在传输的类型有 Content-Type 加以标记

HTTP 协议具有以下缺点：

- 无状态：HTTP 是一个无状态的协议，HTTP 服务器不会保存关于客户的任何信息

- 明文传输：协议中的报文使用的是文本形式，这就直接暴露给外界，不安全

- 不安全：通信使用明文(不加密)，内容可能会被窃听；不验证通信方的身份，因此有可能遭遇伪装；证明报文的完整性，所以有可能已遭篡改

# URI、URL、URN 分别是什么?

URL 代表资源的路径地址，而 URI 代表资源的名称

URI：Universal Resource Identifier 统一资源标识符

URL：Universal Resource Locator 统一资源定位符。URL 类似于住址，它告诉你一种寻找目标的方式

URN：Universal Resource Name 统一资源名称。可以把一个人的名字看作是 URN，因此可以用 URN 来唯一标志一个实体

URL 是 URI 的一个子集，告诉我们访问网络位置的方式；URN 是 URI 的子集，包括名字(给定的命名空间内)，但是不包括访问方式

URN 和 URL 都是 URI 的子集

# TS 中 never 和 void 的区别?

- void 表示没有任何类型(可以被赋值为 null 和 undefined)

- never 表示一个不包含值的类型，即表示永远不存在的值

- 拥有 void 返回值类型的函数就能正常运行。拥有 never 返回值类型的函数无法正常返回，无法终止，或会抛出异常

# 如何保存页面的当前状态？

### 组件会被卸载

1.将状态存储在 LocalStorage/SessionStorage

优点：

兼容性好，不需要额外库或工具

简单快捷，基本可以满足大部分需求

缺点：

- 状态通过 JSON 方法储存(相当于深拷贝)，如果状态中有特殊情况(例如 Date 对象，Regexp 对象等)的时候会得到字符串而不是原来的值 -- JSON 深拷贝的缺点

- 如果 B 组件后台或者下一页跳转并不是前组件，那么 flag 判断会失效，导致从其他页面进入 A 组件页面时，A 组件会重新读取 Storage，会造成很奇怪的现象

2.路由传值

优点：

- 简单快捷，不会污染 LocalStorage/SessionStorage

- 可以传奇 Date、RegExp 等特殊对象

缺点：

- 如果 A 组件可以跳转多个组件，那么在每一个跳转组件内都要写相同的逻辑

### 组件不会被卸载

1.单页面渲染

优点：

- 代码量少

- 不需要考虑状态传递过程中的错误

缺点：

- 增加 A 组件维护成本

- 需要传入额外的 prop 到 B 组件

- 无法利用路由定位页面

2.keep-alive

# 如何从 html 元素继承 box-sizing?

在大多数情况下我们在设置元素的 border 和 padding 并不希望改变元素的 width、height 值，这个时候我们就可以为该元素设置 box-sizing:border-box;

如果不希望每次都重写一遍，而是希望它是继承过来的，那么我们可以使用如下代码：

```
html {
  box-sizing: border-box;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}
```

这样的好处在于它不会覆盖其他组件的 box-sizing 值，又无需为每一个元素重复设置 box-sizing:border-box;

# 微前端可以解决什么问题？

任何新技术的产生都是为了解决现有场景和需求下的技术痛点，微前端也不例外：

- 拆分和细化
当下前端领域，单页面应用(SPA)是非常流行的项目形态之一。而随着时间的推移以及应用功能的丰富，单页应用变得不再单一而是越来越庞大也越来越难以维护，往往是改一处而动全身，由此带来的发版成本也越来越高。微前端的意义就是将这些庞大应用进行拆分，并随之解耦，每个部分可以单独进行维护和部署，提升效率

- 整合历史系统
在不少的业务中，或多或少会存在一些历史项目，这些项目大多以采用老框架类似(Backbone.js，Angular.js)的 B 端管理系统为主，介于日常运营，这些系统需要结合到新框架中使用还不能抛弃，对此我们也没有将这些系统进行整合，在基本不修改逻辑的同时来兼容新老两套系统并行运行

微前端架构具备以下核心价值：
- 技术栈无关
主框架不限制接入应用的技术栈，微应用具备完全自主权

- 独立开发，独立部署
微应用仓库独立，前后端可独立开发，部署完成后主框架自动完成同步更新

- 增量升级
在面对各种复杂场景时，我们通常很难对一个已经存在的系统做全量的技术栈升级或重构，而微前端是一种非常好的实施渐进式重构的手段和策略

- 独立运行时
每个微应用之间状态隔离，运行时状态不共享

# 协商缓存中，有 Last-Modified，为什么还会出现 ETag?

ETag 的出现，主要是为了解决 Last-Modified 无法解决的一些问题：

- 某些服务器不能精确得到文件的最后修改时间，这样就无法通过最后修改时间来判断文件是否更新了。

- 某些文件的修改非常频繁，在秒以下的时间内进行修改，Last-Modified 只能精确到秒

- 一些文件的最后修改时间改变，但内容并未改变，我们不希望客服端认为这个文件修改了

# JS 中怎么阻止事件冒泡和默认事件？

- event.stopPropagation()

这是阻止事件的冒泡方法，不让事件向 document 上蔓延，但是默认事件任然会执行，当你调用这个方法的时候，如果点击一个连接，这个连接仍然会被打开

- event.preventDefault()

这是阻止默认事件的方法，比如在 a 标签的绑定事件上调用此方法，连接则不会打开，但是会发生冒泡，冒泡会传递到上一层的父元素

- return false

这个方法比较暴力，它同时会阻止事件冒泡和默认事件；如果带上这行代码，连接不会被打开，事件也不会传递到上一层的父元素，可以理解为 return false 就等同于同时调用 event.stopPropagation()和 event.preventDefalut()

# 如何使用 css 来实现禁止移动端页面的左右滑动手势?

1.CSS 属性touch-action用于设置触摸屏用户如何操作元素的区域（例如：浏览器内置的缩放功能）

最简单方法是：
```
html {
  touch-action: none;
  touch-action: pan-y;
}
```
还可以直接指定对应元素的宽度和 overflow：
```
html {
  width: 100vw;
  overflow-x: hidden;
}
```

2.使用js监听touch事件，使用event.preventDefault()阻止浏览器的默认行为

# 什么是 JSX?

JSX是一种JavaScript的语法扩展，全称JavaScript XML，运用于React架构中，其格式比较像是模版语言，但事实上完全是在JavaScript内部实现的。元素是构成React应用的最小单位，JSX就是用来声明React当中的元素，React使用JSX来描述用户界面，能让我们可以在JS中写html标记语言。

优点：

- 允许使用熟悉的语法来定义 HTML 元素树

- 提供更加语义化且易懂的标签

- 程序结构更容易被直观化

- 抽象 React Element 的创建过程

- 可以随时掌控 HTML 标签以及生成这些标签的代码

- 是原生的 JavaScript

# 为什么推荐使用 TypeScript?

TypeScript 是微软公司开发和维护的一种面向对象的编程语言。它是 JavaScript 的超集，包含其所有元素。强类型和弱类型、静态类型和动态类型是两组不同的概念。类型强弱是针对类型转化是否显示来区分，静态和动态类型是针对类型检查的时机来区分

TS 对 JS 的改进主要是静态类型检查，静态类型检查有何意义? 标准答案：静态类型更有利于搭建大型应用。

推荐使用 TS 的原因有：

- TS 简化 JS 代码，使其更易于阅读和调试

- TS 是开源的

- TS 为 JS ide 和实践(如静态检查)提供了高效的开发工具

- TS 使代码更易于阅读和理解

- 使用 TS，我们可以大大改进普通的 JS

- TS 为我们提高 ES6 的所有优点和更高的生产率，节省开发人员的实践

- TS 通过对代码进行类型检查，可以帮助我们避免在编写 JS 时经常遇到令人痛苦的错误

- 强大的类型系统，包括泛型

- TS 只不过是带有一些附加功能的 JS

- TS 代码可以按照 ES5 和 ES6 标准编译，来支持最新的浏览器

- 与 ECMAScript 看齐来实现兼容性，TS 是 ES3 ES5 和 ES6 的超集

- 支持静态类型

总结：使用 TypeScript，减少运行时错误，降低测试和维护成本。

# TS 中 any 和 unknown 有什么区别?

unknown和any都是TS中的顶级类型，但主要区别在于：使用any相当于彻底放弃了类型检查，而unknown类型相较于any更加严格，在执行大多数操作之前，会进行某种形式的检查。unknown 因为未知性质，不允许访问属性，不允许赋值给其他有明确类型的变量。

# 说说你在 React 项目是如何捕获错误的?

# 为什么说 HTTP 是无状态协议?

因为它的每个请求都是完全独立的，每个请求包含了处理这个请求所需的完整的数据。

无状态协议是指协议对务处理没有记忆功能。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。HTTP 协议不像建立 socket 连接的两个终端，双方是可以互相通信的。HTTP 的客户端只能通过请求服务器来获取相关内容或文件信息

HTTP 协议这种特性有优点也有缺点，优点在于解放服务器，每一次请求点到为止，不会造成不必要连接占用，缺点在于每次请求会传输大量重复的内容信息

在同一个连接允许传输多个 HTTP 请求的情况下，如果第一个请求出错了，后面的请求一般也能够继续处理(当然，如果导致协议解析失败、消息分片错误之类的自然是要除外的)可以看你出，这种协议的结构是要比有状态的协议更简单的

# React 中懒加载的实现原理是什么?

# React 中，父子组件的生命周期执行顺序是怎么样的?

React 的生命周期从广义上分为三个阶段：挂载、渲染、卸载，因此可以把 React 的生命周期分为两类：挂载卸载过程和更新过程。

#### 挂载卸载过程
constructor 完成 React 数据的初始化

componentWillMount 组件初始化数据后，但是还未渲染 DOM 前

componentDidMount 组件第一次渲染完成，此时 dom 节点已经生成

componentWillUnmount 组件的卸载和数据的销毁

#### 更新过程
componentWillReceiveProps(nextProps) 父组件改变后的 props 需要重新渲染组件时

shouldComponentUpdate(nextProps，nextState) 主要用于性能优化(部分更新)，因为 react 父组件的重新渲染会导致其所有子组件的重新渲染，这个时候其实我们是不需要所有子组件都跟着重新渲染的，在这里 return false 可以阻止组件的更新

componentWillUpdate(nextProps,nextState) shouldComponentUpdate 返回 true 后，组件进入重新渲染的流程

componentDidUpdate(prevProps,prevState) 组件更新完毕后触发

render() 渲染时触发

#### 父子组件加载顺序
观察父子组件的挂载生命周期函数，可以发现挂载时，子组件的挂载钩子先被触发；卸载时，子组件的卸载钩子后被触发

我们经常在挂载函数上注册监听器，说明此时是可以与页面交互的，也就是说其实所有挂载钩子都是在父组件实际挂载到 dom 树上才触发的，不过是在父组件挂载后依次触发子组件的 componentDidMount，最后在触发自身的挂载钩子，说白了，componentDidMount 其实是异步钩子。相反，卸载的时候父节点先被移除，在从上至下依次触发子组件的卸载钩子

但是我们也经常在卸载钩子上卸载监听器，这说明 componentWillUnmount 其实在父组件从 dom 树上卸载前触发的，先出发自身的卸载钩子，但此时并未从 dom 树上剥离，然后依次尝试触发所有子组件的卸载钩子，最后，父组件从 dom 树上完成实际卸载

# css sprites 是什么?怎么使用?

css sprites 是一种网页图片应用处理方式，就是把网页中一些背景图片整合到一张图文件中，在利用 css 的 background-image、background-repeat、background-position 的组合进行背景定位以提高性能，也被称为css精灵图。

优点：

- 减少网页的 http 请求，提高性能，这也是 css sprites 最大的优点，也是其被广泛传播和应用的主要原因

- 减少图片的字节：多张图片合并成一张图片的字节小于多张图片的字节总和

- 减少了命名困扰：只需对一张集合的图片命名，不需要对每一个小元素进行命名提高制作效率

- 更换风格方便：只需要在一张或少张图片上修改图片的颜色或样式，整个网页的风格可以改变，维护起来更加方便

缺点：

- 图片合成比较麻烦

- 背景设置时，需要得到每一个背景单元的精确位置

- 维护合成图片时，最好只是往下加图片，而不要更改已有图片

# 什么是 TypeScript Declare 关键字？

TypeScript declare 关键字用于方法或变量的环境声明。我们知道所有的 JS 库/框架都没有 TS 声明文件，但是我们希望在 TS 文件中使用它们时不会出现编译错误。为此，我们使用 declare 关键字。在我们希望定义可能存在于其他地方的变量的环境声明和方法中，可以使用 declare 关键字。

# 简单介绍下 ES6 中的 Iterator 迭代器

Iterator 迭代器就是一个接口方法，它为不同的数据结构提供了一个统一的访问机制；使得数据结构的成员能够按某种次序排序，并逐个被访问

# 页面导入样式时，使用 link 和@import 有什么区别？

两者都是外部引用 css 的方式，它们的区别如下：

- link 是 XHTML 标签，除加载 css 之外，还可以定义 RSS 等其他事务；@import 属于 css 范畴，只能加载 css

- link 引用 css 时，在页面载入时同时加载；@import 需要页面网页完全载入以后加载

- link 是 XHTML 标签，无兼容问题；@import 是在 css2.1 提出的，低版本的浏览器不支持

- link 支持使用 javascript 控制 DOM 去改变样式；而@import 不支持

# URI 和 URL 的区别

URL是统一资源定位器，用于标识资源；URI（统一资源标识符）提供了更简单和可扩展的标识资源的方法。URL是URI的子集。

1、作用的区别

URL（统一资源定位符）主要用于链接网页，网页组件或网页上的程序，借助访问方法（http，ftp，mailto等协议）来检索位置资源。

URI（统一资源标识符）用于定义项目的标识，此处单词标识符表示无论使用的方法是什么（URL或URN），都要将一个资源与其他资源区分开来。

2、可以说URL是URI（URL是URI的子集），但URI永远不能是URL。

3、协议区别

URL指定要使用的协议类型，而URI不涉及协议规范

# 两个同级的相邻元素之间，有看不见的空白间隔，是什么原因引起的?有什么解决办法?

行框的排列也会受到中间空白(回车空格)等的影响，因为空格也属于字符，这些空包也会被应用样式，占据空间，所以会有间隔，把字符大小设为 0，就没有空格了

解决办法：

- 把相邻元素代码全部写成一排

- 浮动元素，float:left

- 在父级元素中用 font-size:0

# TypeScript 的主要特点是什么?

- 跨平台：TypeScript 编译器可以安装在任何操作系统上，包括 windows、macOS 和 Linux

- ES6 特性：TypeScript 包含计划中的 ES6 的大部分特性，例如箭头函数

- 面向对象的语言：TS 提供所有标准的 OOP 功能，如类、接口和模块

- 静态类型检查：TypeScript 使用静态类型并帮助在编译时进行类型检查。因此，你可以在编写代码时发现编译时错误而无需运行脚本

- 可选的静态类型：如果你习惯了 JS 的动态类型，TypeScript 还允许可选的静态类型

- DOM 操作：你可以使用 TypeScript 来操作 DOM 以添加或删除客户端网页元素

# 说说对 ES6 中 rest 参数的理解

ES6 引入 rest 参数(形式为…变量名)，用于获取函数的多余参数，这样就不需要使用 argument 对象。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。argument 对象不是数组，而是一个类似数组的对象。所以为使用数组的方法，必须使用 Array.peototype.slice.call 先将其转为数组。rest 参数就不存在这个问题，它就是一个真正的数组，数组特有的方法都可以使用。

# 前端的常规安全策略有哪些?

[前端存储和安全策略](https://zhuanlan.zhihu.com/p/375433739)

# 请简述下什么是面向对象?

面向对象是一种思想，是基于面向过程而言的，就是说面向对象是将功能等通过对象来实现，将功能封装进对象之中，让对象去实现具体的细节；这种思想是将数据作为第一位，这是对数据一种优化，操作起来更加的方便，简化流程。JS 本身是没有 class 类型的，但是每个函数都有一个 prototype 属性，prototype 指向一个对象，当函数作为构造函数时，prototype 就起到类似于 class 的作用

面向对象有三个特点：封装(隐藏对象的属性和实现细节，对外提供公共访问方式)，继承(提高代码复用性，继承是多态的前提)，多态(是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象)

# Redux 中异步的请求怎么处理?

Redux 中 Reducer 必须是同步函数，因此异步处理会放到中间件中去做。Redux 中间件实质是 store.dispatch 函数的增强器，它们拦截特定的 Action，并在其中把带有副作用的工作完成。常见的异步处理中间件有：redux-thunk、redux-saga、redux-promise 等

# 如何用 webpack 来优化前端性能？

1. 压缩代码：删除多余的代码、注释、简化代码的写法等方式；比如，利用 webpack 的 UglifyJsPlugin 和 ParallelUglifyPlugin 来压缩 js ⽂件， 利⽤ cssnano （css-loader?minimize）来压缩css
2. 利用 CDN 加速：在构建过程中，将引⽤的静态资源路径修改为CDN上对应的路径。可以利⽤webpack对于 output 参数和各loader的 publicPath 参数来修改资源路径
3. Tree Shaking：将代码中永远不会⾛到的⽚段删除掉。可以通过在启动webpack时追加参数 --optimize-minimize 来实现
4. Code Spliting：将代码按路由维度或者组件分块(chunk),这样做到按需加载,同时可以充分利⽤浏览器缓存
5. 提取公共第三方库：SplitChunksPlugin插件来进⾏公共模块抽取,利⽤浏览器缓存可以⻓期缓存这些⽆需频繁变动的公共代码

# webpack、rollup、parcel 的优劣是什么？

| 对比      | webpack | rollup | parcel |
| ----------- | ----------- | ----------- | ----------- |
| 功能      | 为处理资源管理和分割代码而生，可以用来处理任何类型的文件，灵活，插件多       | 用标准化的格式（es6）来写代码，通过减少死代码尽可能地缩小包体积      | 用标准化的格式（es6）来写代码，通过减少死代码尽可能地缩小包体积      |
| 配置   | webpack需要配config文件，指明entry, output, plugin，transformations        | rollup需要配config文件，指明entry, output, plugin，transformations。rollup 有对import/export所做的node polyfills，webpack没有。rollup支持相对路径，而webpack没有，所以得使用path.resolve/path.join        | parcel则是完全开箱可用的，不用配置        |
| 入口文件   | webpack只支持js文件作为入口文件，如果要以其他格式的文件作为入口，比如html文件为入口，如要加第三方Plugin        | rollup可以用html作为入口文件，但也需要plugin，比如rollup-plugin-html-entry   | parcel可以用index.html作为入口文件，而且它会通过看index.html的script tag里包含的什么自己找到要打包生成哪些js文件   |
| transformations   | transformations指的是把其他文件转化成js文件的过程，需要经过transformation才能够被打包。webpack使用Loaders来处理        | rollup使用plugins来处理   | parcel会自动去转换，当找到配置文件比如.babelrc, .postcssrc后就会自动转   |
| tree shaking   | tree shaking 优化是webpack的一大特性。需要1，用import/export语法，2，在package.json中加副作用的入口，3，加上支持去除死代码的缩小器（uglifyjsplugin）        | rollup会统计引入的代码并排除掉那些没有被用到的。这使您可以在现有工具和模块的基础上构建，而无需添加额外的依赖项或膨胀项目的大小   | parcel不支持摇树优化   |
| dev server   | webpack用webpack-dev-server        | rollup用rollup-plugin-serve和rollup-plugin-livereload共同作用   | parcel内置的有dev server   |
| 热更新   | webpack的 wepack-dev-server支持hot模式        | rollup不支持hmr   | parcel有内置的hmr   |
| 代码分割   | webpack通过在entry中手动设置，使用CommonsChunkPlugin，和模块内的内联函数动态引入来做代码分割        | rollup有实验性的代码分割特性。它是用es模块在浏览器中的模块加载机制本身来分割代码的。需要把experimentalCodeSplitting 和 experimentalDynamicImport 设为true   | parcel支持0配置的代码分割。主要是通过动态improt   |

# 简述 Vue 模板编译原理

Vue 中的模板 tempalte 无法被浏览器解析并渲染，因为这不属于浏览器的标准，不是正确的 HTML 语法，所以需要将 template 转化成一个 JS 函数，这样浏览器就可以执行这一个函数并渲染出对应的 HTML 元素，就可以让试图跑起来，这是一个转化的过程，就成为模板编译。模板编译又分为三个阶段：解析 parse、优化 optimize，生成 genertate，最终生成可执行函数 render

- 解析阶段：使用大量的正则表达式对 template 字符串进行解析，将标签、指令、属性等转化为抽象语法树 AST

- 优化阶段：遍历 AST，找到其中的一些静态节点并进行标记，方便在页面重渲染的时候进行 diff 比较时，直接跳过这一些静态节点，优化 runtime 性能

- 生成阶段：将最终的 AST 转化成 render 函数字符串

# 对于定长和不定长的数据，HTTP 是怎么传输的?

定长：对于定长包体而言，发送端在传输的时候一般会带上 Content-Length，来指明包体的长度。

不定长： http 头部字段——Transfer-Encoding: chunked。表示分块传输数据，设置这个字段后会自动产生两个效果:

- Content-Length 字段会被忽略
- 基于长连接持续推送动态内容

# 什么是 DNS 劫持?

DNS 劫持是常见的网络攻击方式，它会对网站的流量、权重产生影响，甚至会让用户置身于危险中，泄露隐私造成财产损失。DNS 即 域名系统，它是用来解析域名的。
当网站经过本地 DNS 解析时，黑客将本地 DNS 缓存中国呢的目标网站替换成其他网站的 IP 返回，而客户端并不知情，依旧按照正常流程寻址建立并连接。这样就可以做很多的坏事了，比如 DDos 攻击、DNS 缓存感染、信息劫持、 ARP欺骗等

# 如何实现浏览器内多个标签页之间的通信?

- Broadcast Channel：用于同源不同页面之间完成通信的功能，在其中某个页面发送的消息会被其他页面监听到

- localStorage：浏览器多个标签共用的存储空间，所以可以用来实现多标签之间的通信(session 是会话级的存储空间，每个标签页都是单独的)

- WebSocket：通讯全双工(full-duplex)通信自然可以实现多个标签之间的通信

- postMessage：两个需要交互的 tab 页面具有依赖关系

# document.write 和 innerHTML 的区别？

document.write 是直接写入页面的内容流，如果在写之前没有调用document.open，浏览器会自动调用open。每次写完关闭后重新调用该函数，会导致页面重写，这个方法是重写整个document，写入内容是字符串的html

innerHTML 是DOM页面元素的一个属性，代表该元素的html内容。不会导致页面重绘，它是 HTMLElement 的属性，是一个元素的内部 html 内容。



# React 中怎么实现状态自动保存(KeepAlive)?

在 React 中，我们通常会使用路由去管理不同的页面，而在切换页面时，路由将会卸载掉未匹配的页面组件。当我们在临时离开交互场景，需要对状态进行保存。常见的解决方式：

1. 手动保存状态：配合 react 的生命周期 和 redux 状态管理对状态进行记录，返回场景时进行数据恢复
2. 通过路由实现自动状态保存：可以使用 react-keep-alive 或 react-router-cache-route

# 了解 React 中的 ErrorBoundary 吗，它有哪些使用场景?

ErrorBoundary可以在任务子组件中捕获js错误，只需在根组件中定义一次，即可捕获所有子组件的错误。其实就是在整个 workloop 外面包一层 try catch，报错的时候遍历父组件找到这两个生命周期并把堆栈信息塞给生命周期进行判断

但以下4种错误除外：

1. 事件处理函数中使用try catch
2. 异步函数（setTimeout）
3. 服务端渲染
4. 当前ErrorBoundary抛出的错误 

# Composition API 与 React Hooks 很像，区别是什么?

从 React Hook 的实现角度看，React Hook 是根据 useState 调用的顺序来确定下一次重渲染时的 state 是来源于哪个 useState，所以出现了以下限制：

- 不能再循环、条件、嵌套函数中调用 Hook

- 必须确保总是在你的 React 函数的顶层调用 Hook

- useEffect、useMemo 等函数必须手动确定依赖关系

而 Composition API 是基于 Vue 的响应式系统实现的，与 React Hook 相比：

- 声明在 setup 函数内，一次组件实例化只调用一次 setup，而 React Hook 每次重渲染都需要调用 Hook，使得 React 的 GC 比 Vue 更有压力，性能也行对于 Vue 来说比较慢

- Composition API 的调用不需要考虑调用顺序，也可以在循环、条件、嵌套函数中使用

- 响应式系统自动实现依赖收集原理，进而组件部分的性能优化由 Vue 内部自己完成，而 React Hook 需要手动传入依赖，且必须保证依赖的顺序，让 useEffect、useMemo 等函数正确的捕获依赖变量，否则会由于依赖不正确使得组件性能下降

虽然 Composition API 看起来比 React Hook 好用，但其设计思想也是借鉴 React Hook 的

# 正向代理和反向代理分别是什么？

- 正向代理

正向代理即隐藏真实的客户端，客户端请求的服务都被代理服务器代替来请求。它是一个位于客户端和原始服务器之前的服务器，为了从原始服务器取得内容，客户端向代理发送一个请求并且指定目标（原始服务器），然后代理向原始服务器转交请求并将获得的内容返回给客户端，客户端才能使用正向代理
  
- 反向代理

反向代理隐藏真实服务端。反向代理服务器位于用户与目标服务器之间，但是对于用户而言，反向代理服务器就相当于目标服务器，即用户直接访问反向代理服务器就可以获得目标服务器的资源。反向代理服务器通常可用来作为Web加速，即使用反向代理作为Web服务器的前置机来降低网络和服务器的负载，提高访问效率。Nginx就是性能非常好的反向代理服务器，用来做负载均衡。

- 区别

正向代理代理的对象是客户端，反向代理代理的对象是服务端。正向代理中，proxy和client同属一个LAN，对server透明；反向代理中，proxy和server同属一个LAN，对client透明。

# 简述下 overflow 的原理

要知道这个原理，首先要清楚什么是块格式化上下文（BFC）。BFC 是 CSS 可视化渲染的一部分，它定义了一块独立的渲染区域，规定了其内部块级元素的渲染规则，其渲染效果不受外界环境的干扰。当元素设置了 overflow 样式且值不为 visible 时，该元素就构建了一个 BFC。

BFC定义了如下布局规则：

- 内部的块元素会在垂直方向，一个接一个地放置

- 块元素垂直方向的距离由 margin 决定，两个相邻块元素的垂直方向的 margin 会发生重叠

- 每个元素的左外边距，与包含块的左边相接触(对于从左往右的格式化，否则相反)，即使存在浮动也是如此

- BFC 的区域不会与 float 元素的区域重叠

- BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也如此

- 计算 BFC 的高度时，浮动元素也参与计算，也就是说 BFC 区域内只有一个浮动元素，BFC 的高度也不会发生塌缩，所以达到了清除浮动的目的

# WebSocket 是如何进行握手的?

# WebSocket 与 HTTP 有什么关系?

WebSocket 是一种与 HTTP 不同的协议。两者都位于 OSI 模型的应用层，并且都依赖于传输层的 TCP 协议。虽然它们不同，但是 RFC 6455 中规定: WebSocket 被设计为在 HTTP 80 和 443 端口上工作，并支持 HTTP 代理和中介，从而使其与 HTTP 协议兼容。为了实现兼容性，WebSocket 握手使用 HTTP Upgrade 头，从 HTTP 协议更改为 WebSocket 协议。

# new 的原理是什么?通过 new 的方式创建对象和通过字面量创建有什么区别?

new操作符的作用如下：

1.创建一个空对象

2.由this变量引用该对象

3.该对象继承该函数的原型

4.把属性和方法加入到this引用的对象中

5.新创建的对象由this引用，最后隐式地返回this。

new创建对象和字面量创建本质上是一样的，字面量的方式比较简单，也不用调用构造函数，性能较好

# 描述下你所理解的 postcss 作用

postcss 提供了一个解析器，能够将 css 解析成抽象语法树。通过在 postcss 这个平台上开发一些插件来处理css，比如，autoprefixer。postcss 可以对 sass 处理过的 css 再进行处理，比如 autoprefixer

# 简述一下 src 和 href 的区别

href：是指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接；如果我们在文档中添加 <link href="min.css" rel="stylesheet"/> 那么浏览器会识别该文档为 css 文件，就会并行下载资源并且不会停止对当前文档的处理,这也是为什么建议使用 link 方式来加载 css，而不是使用 @import 方式。

src：是指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置（替换当前元素）；在请求src资源时会将其指向的资源下载并应用到文档内，例如 js 脚本，img 图片和 frame 等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理（同步操作），直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将 js 脚本放在底部而不是头部。

# 能描述下渐进增强和优雅降级之间的不同么？

- 渐进增强（progressive enhancement）：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级（graceful degradation）：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容
- 区别：优雅降级是从复杂的现状开始的，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始并不断进行扩充，来适应未来环境的需要

# 常见的兼容性问题有哪些?

- 不同的浏览器的默认标签的 margin 和 padding 不一样。 `*{margin:0;padding:0;}`
- IE6 双边距：块属性标签 float 后，又有横行的 margin 情况下，在 IE6 显示 margin 比设置的大。 `hack：display:inline将其转化为行内属性`
- 设置较小高度标签(一般小于 10px)，在 IE6，IE7 中高度超出自己设置高度。hack：给超出高度的标签设置 overflow:hidden;或者设置行高 line-height 小于你设置的高度
- IE 下，可以使用获取常规属性的方法来获取自定义属性，也可以使用 getAttribute()获取自定义属性；Firefox 下，只能使用 getAttribute()获取自定义属性。
  - 解决方法：统一通过 getAttribute()获取自定义属性
- Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示，可通过加入 CSS 属性 `-webkit-text-size-adjust: none; ` 解决
- 超链接访问过后 hover 样式就不出现了，被点击访问过的超链接样式不再具有 hover 和 active 了。解决方法是改变 CSS 属性的排列顺序: `L-V-H-A ( love hate ): a:link {} a:visited {} a:hover {} a:active {}`

# 什么情况会阻塞渲染?

- html和css生成渲染树的过程
- 解析script标签，DOM暂停构建

# instanceof 的原理是什么

instanceof 运算符用于测试构造函数的 prototype 属性是否出现在对象原型链中的任何位置

实现：
```
function instanceof(left, right) {
  const RP = right.prototype; // 构造函数的原型
  while(true) {
    if (left === null) {
      return false;
    }
    if (left === RP) { // 一定要严格比较
      return true;
    }
    left = left.__proto__; // 沿着原型链重新赋值
  }
}
复制代码
```

# 你所了解的网页制作用到的图片格式有哪些?

png-8, png-24, jpeg, gif, gif, svg, webp 等

# 请列出 HTTP/1.1 协议 Response 状态码: 20x、30x、40x、 50x 等各区间的含义，并说明 Action 在 Restful API 中分别使用哪些 HTTP 副词表现出 CRUD?
```
HTTP/1.1 协议 Response 状态码: 20x、30x、40x、 50x 等各区间的含义
20x：成功处理请求

30x：重定向请求

40x：请求错误

50x：服务器错误

20x 详细状态=> 200(成功), 201(已创建), 202(已接受), 203(非授权), 204(无内容), 205(重置内容), 206(部分内容)

30x 详细状态=> 300(多种选择), 301(永久移动)，302(临时移动), 303(查看其他位置), 304(未修改),305(代理), 307(临时重定向)

40x 详细状态=> 400(错误), 401(未授权), 403(禁止),404(未找到), 405(方法禁用), 406(不接受), 407(需代理授权), 408(请求超时), 409(冲突), 410(已删除),411(需要有效长度), 412(未满足条件), 413(请求实体过大)，414(请求 URI 过长), 415(不支持的媒体类型), 416(请求范围不合要求),417(未满足期望值),428(请求先决条件), 429(太多请求), 431(请求字段太大)

50x 详细状态=> 500 (服务器内部错误)，501(尚未实施)，502(错误网管), 503(服务不可用), 504(网关超时),505(HTTP 版本不受支持), 511(要求网络认证)

说明 Action 在 Restful API 中分别使用哪些 HTTP 副词表现出 CRUD
GET:从服务器获取资源(查)

POST:在服务器创建资源(增)

PUT:在服务器更新资源(改)，一般是完整更新 =>PATCH(改)，改变资源部分属性

DELET:在服务器删除资源(删)
```

# 通过什么做到并发请求?

# 最后一个单词的长度
```
给你一个字符串 s，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中最后一个单词的长度。

单词 是指仅由字母组成、不包含任何空格字符的最大子字符串。


示例 1：

输入：s = "Hello World"
输出：5


示例 2：

输入：s = "   fly me   to   the moon  "
输出：4


示例 3：

输入：s = "luffy is still joyboy"
输出：6


var lengthOfLastWord = function(s) {
    if (!s) return 0
    let arr = s.trim().split(' ')
    return arr[arr.length - 1].length
};
```

# 详细说一下你对 cookie、session、token 的理解

# Socket 是什么?

# 数组序号转换
```给你一个整数数组&nbsp;arr ，请你将数组中的每个元素替换为它们排序后的序号。

序号代表了一个元素有多大。序号编号的规则如下：

序号从 1 开始编号。
一个元素越大，那么序号越大。如果两个元素相等，那么它们的序号相同。
每个数字的序号都应该尽可能地小。
&nbsp;

示例 1：

输入：arr = [40,10,20,30]
输出：[4,1,2,3]
解释：40 是最大的元素。 10 是最小的元素。 20 是第二小的数字。 30 是第三小的数字。
示例 2：

输入：arr = [100,100,100]
输出：[1,1,1]
解释：所有元素有相同的序号。
示例 3：

输入：arr = [37,12,28,9,100,56,80,5,12]
输出：[5,3,4,2,8,6,7,1,3]

var arrayRankTransform = function(arr) {
    // TODO
};
```

# 客户端如何发送 http 请求？

# 介绍 defineProperty 方法，什么时候需要用到?

# 存在连续三个奇数的数组
```
给你一个整数数组 arr，请你判断数组中是否存在连续三个元素都是奇数的情况：如果存在，请返回 true ；否则，返回 false 。

示例 1：

输入：arr = [2,6,4,1]
输出：false
解释：不存在连续三个元素都是奇数的情况。


示例 2：

输入：arr = [1,2,34,3,4,5,7,23,12]
输出：true
解释：存在连续三个元素都是奇数的情况，即 [5,7,23] 。

var threeConsecutiveOdds = function(arr) {
    // TODO
};
```

# HTTP 连接是如何复用的?

# 前后端通信使用什么方案?

# 最长公共前缀
```
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串&nbsp;""。


示例 1：

输入：strs = ["flower","flow","flight"]
输出："fl"


示例 2：

输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。


var longestCommonPrefix = function(strs) {
    // TODO
};
```

# 说一下你了解的 WebSocket 鉴权授权方案?

# 说一下错误监控的实现，错误监控的正确使用方式，日志如何分等级?

# 实现 strStr()

# tcp 和 udp 有什么区别？tcp 怎样确保数据正确性？

# 传输层和网络层分别负责什么，端口在什么层标记

# DOM tree 和 CSS tree 是如何合并成 render tree 的？

# 原生 JS 实现图片懒加载的思路
实现方案:

1. 在 img 元素时，自定义一个属性 data-src，用于存放图片的地址

2. 获取屏幕可视区域的尺寸

3. 获取元素到窗口边缘的距离

4. 判断元素时候在可视区域内，在的话则 data-src 的值赋给 src；否则不执行其他操作

本质：当图片在可视区域内时才会加载否则不加载；也可以给一个默认的图片占位。

# 颜色分类
```
给定一个包含红色、白色和蓝色，一共&nbsp;n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、&nbsp;1 和 2 分别表示红色、白色和蓝色。


示例 1：

输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]


示例 2：

输入：nums = [2,0,1]
输出：[0,1,2]


示例 3：

输入：nums = [0]
输出：[0]


示例 4：

输入：nums = [1]
输出：[1]


var sortColors = function(nums) {
//TODO
};
```

# 有 1000 个 dom，需要更新其中的 100 个，如何操作才能减少 dom 的操作？

# 如果在控制台中运行以下函数，页面的 UI 是否仍然响应？
```
function foo() {
  return Promise.resolve().then(foo);
}
```

# 验证栈序列

# encoding 头都有哪些编码方式？

# 把 10 万次 for 循环的代码插到 html 中间，会有什么现象？出现卡顿现象怎么解决？添加 defer 属性之后脚本会出在什么时候来执行？采用 defer 之后，用户点击页面会怎样？如果禁用 WebWoker，还有其他解决办法么？

# 亲密字符串
```
给你两个字符串 s 和 goal ，只要我们可以通过交换 s 中的两个字母得到与 goal 相等的结果，就返回&nbsp;true&nbsp;；否则返回 false 。

交换字母的定义是：取两个下标 i 和 j （下标从 0 开始）且满足 i != j ，接着交换 s[i] 和 s[j] 处的字符。

例如，在 "abcd" 中交换下标 0 和下标 2 的元素可以生成 "cbad" 。

示例 1：

输入：s = "ab", goal = "ba"
输出：true
解释：你可以交换 s[0] = 'a' 和 s[1] = 'b' 生成 "ba"，此时 s 和 goal 相等。


示例 2：

输入：s = "ab", goal = "ab"
输出：false
解释：你只能交换 s[0] = 'a' 和 s[1] = 'b' 生成 "ba"，此时 s 和 goal 不相等。


示例 3：

输入：s = "aa", goal = "aa"
输出：true
解释：你可以交换 s[0] = 'a' 和 s[1] = 'a' 生成 "aa"，此时 s 和 goal 相等。


示例 4：

输入：s = "aaaaaaabc", goal = "aaaaaaacb"
输出：true

var buddyStrings = function(s, goal) {
    if (s.length !== goal.length) return false;
    if (s === goal) {
        let arr = s.split('');
        if ([...new Set(arr)].length !== s.length) return true;
        return false;
    }
    let a = -1;
    let b = -1;
    for(let i = 0; i < s.length; i++){
        if(s[i] !== goal[i]){
            if(a === -1){
                a = i;
            }else if(b === -1){
                b = i;
            }else {
                return false;
            }
        }
    }
    return b !== -1 && s[a] == goal[b] && s[b] == goal[a];
};
```

# 多个 tab 只对应一个内容框，点击每个 tab 都会请求接口并渲染到内容框，怎么确保频繁点击 tab 但能够确保数据正常显示？

# 什么是 http？什么是 http2？说下 http 和 http2 的工作流程？

# O(1) 时间插入、删除和获取随机元素
```
实现RandomizedSet 类：

RandomizedSet() 初始化 RandomizedSet 对象
bool insert(int val) 当元素 val 不存在时，向集合中插入该项，并返回 true ；否则，返回 false 。
bool remove(int val) 当元素 val 存在时，从集合中移除该项，并返回 true ；否则，返回 false 。
int getRandom() 随机返回现有集合中的一项（测试用例保证调用此方法时集合中至少存在一个元素）。每个元素应该有 相同的概率 被返回。
你必须实现类的所有函数，并满足每个函数的 平均 时间复杂度为 O(1) 。


示例：

输入
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
输出
[null, true, false, true, 2, true, false, 2]

解释
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomizedSet.remove(2); // 返回 false ，表示集合中不存在 2 。
randomizedSet.insert(2); // 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomizedSet.getRandom(); // getRandom 应随机返回 1 或 2 。
randomizedSet.remove(1); // 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomizedSet.insert(2); // 2 已在集合中，所以返回 false 。
randomizedSet.getRandom(); // 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。

var RandomizedSet = function () {

};

/** 
 * @param {number} val
 * @return {boolean}
 */
RandomizedSet.prototype.insert = function (val) {

};

/** 
 * @param {number} val
 * @return {boolean}
 */
RandomizedSet.prototype.remove = function (val) {

};

/**
 * @return {number}
 */
RandomizedSet.prototype.getRandom = function () {

};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * var obj = new RandomizedSet()
 * var param_1 = obj.insert(val)
 * var param_2 = obj.remove(val)
 * var param_3 = obj.getRandom()
 */
 ```
 
# 详细说一下 JSON.stringify 的一些特性？和遍历相比，哪个性能会更高？

# 介绍下数字签名的原理

# tcp 头包含什么？tcp 属于哪一层？

# 字符串解码

# 为什么用 gulp 打包 node?

# 项目中有没有涉及到 Cluster，说一下你的理解。

# 说一下 HTTPS 获取加密密钥的过程

# 既然 vue 通过数据劫持可以精准探测数据在具体的 dom 上变化，为什么还需要虚拟 DOM diff 呢？

# 回文链表

# 说一下 koa-body 原理

# 说一下请求是异步的为什么会造成阻塞?

# 反转链表

```
/*
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
*/
var reverseList = function(head) {
    if (!head || !head.next) return head;

    let prev = null;
    let curr = head;

    while(curr) {
        let next = curr.next;
        curr.next = prev;

        prev = curr;
        curr = next;
    }
    return prev;
};
```
# 为什么扩展 JavaScript 内置对象不是好的做法?

# 说下 webpack Runtime 和 Manifest 代码的作用？

# 说一下实现骨架屏的方案？具体思路？

# 环形链表
```
给定一个链表，判断链表中是否有环。 如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。 如果链表中存在环，则返回 true 。 否则，返回 false 。

示例1： 输入：head = [3,2,0,-4], pos = 1 输出：true 解释：链表中有一个环，其尾部连接到第二个节点。

示例2： 输入：head = [1,2], pos = 0 输出：true 解释：链表中有一个环，其尾部连接到第一个节点。

const hasCycle = function (head) { //TODO };
```

# 说一下什么是运营商劫持？有什么预防措施？
运营商是指那些提供宽带服务的 ISP，包括三大运营商中国电信、中国移动、中国联通，还有一些小运营商，比如长城宽带，他们提供最基础的网络服务。
网络运营商为了卖广告或者其他经济利益，有时候会直接劫持用户的访问，目前比较常见的有两种方式，DNS 劫持和 HTTP 劫持。

## 遇到DNS运营商劫持怎么办?
1.修改 DNS 地址

运营商劫持弹广告，一般是 DNS 劫持，可以通过修改电脑或者手机网络的 DNS 地址，可以在一定程度上解决广告弹窗的问题。比如，改为 114.114.114.114 这样的公共安全 DNS。

2.投诉

打投诉电话。

# 请介绍下装饰者模式，并实现

# 请说说你对 Sparkplug 的理解？

# 说说服务端渲染 SSR

# 了解相交链表？

# webpack 如果使用了 hash 命名，是否每次都会重新生成 hash? 简单说下 webpack 的集中 hash 策略?

# webpack 和 gulp 的优缺点

# git 快照指的是什么?git 的工作区域由哪三个部分组成?在 git 中，如何提交的版本打标签?

# 开发热环境更新的优化方式

# 说下 LRU 算法的原理并手写实现?一般有哪些优化方式?

# 什么情况下会触发 options 请求?

# 为什么 WeakMap 和 WeakSet 的键只能使用对象?在什么场景下使用?

键的这种限制，是为了保证只有通过键对象的引用来取得值。
```
const m = new WeakMap();
m.set({}, 100);
// 由于 {} 没有在其他地方引用，所以在垃圾回收时，这个值也会被回收。

const a = {};
m.set(a, 100);
// 如果使用这种方式，则不会被回收。因为 {} 有 a 变量在引用它。

a = null;
// 将 a 置为空后，m 里的值 100 在垃圾回收时将会被回收。
```
如果用原始值，就无法区分初始化时使用的字符串字面量和初始化之后使用的是一个相等的字符串了。
```
const a = {};
// 在创建对象时，分配了一块内存，并把这块内存的地址传给 a
m.set(a, 100);
// 执行 set 操作时，实际上是将 a 指向的内存地址和 100 关联起来

const a = "abc";
// 由于基本数据类型在传递时，传递的是值，而不是引用。
m.set(a, 100);
// 所以执行 set 操作时，实际上是将新的 'abc' 和 100 关联起来，而不是原来 a 变量指向的那个。
// 那这样就会有问题，m 里存储的永远是没有被引用的键，随时都会被回收。
```

- 应用场景
1.通过 WeakMap 缓存计算结果

2.存储额外的数据

WeakMap 是类似于 Map 的集合，它仅允许对象作为键，并且一旦通过其他方式无法访问它们，便会将它们与其关联值一同删除。

WeakSet 是类似于 Set 的集合，它仅存储对象，并且一旦通过其他方式无法访问它们，便会将其删除。

它们都不支持引用所有键或其计数的方法和属性，仅允许单个操作。

WeakMap 和 WeakSet 被用作主要对象存储之外的辅助数据结构。一旦将对象从主存储器中删除，如果该对象仅被用作 WeakMap 或 WeakSet 的键，那么它将被自动清除。

# 说下你对前端工程化的理解

# 有没有搭建过 CI/CD？说下搭建流程

# 对 gitflow 了解吗？应该如何使用？

# HTTP2.0 多路复用有多好?

# 如果一个页面突然出现一段广告，可能是什么原因，怎么解决?

# ES6 代码转化成 ES5 代码的实现思路是什么?大致说一下 babel 原理?

# git pull --rebase 和 git pull 的区别是什么?

```
git pull = git fetch + git merge FETCH_HEAD

git pull --rebase = git fetch + git rebase FETCH_HEAD
```
merge操作会生成一个新的节点，之前的提交分开显示，merge 操作遇到冲突的时候，当前merge不能继续进行下去。手动修改冲突内容后，add 修改，commit 就可以了

而rebase操作不会生成新的节点，是将两个分支融合成一个线性的提交。如果 rebase 遇到冲突，会中断 rebase，同时会提示去解决冲突。解决冲突后，将修改add后执行`git rebase –continue`继续操作，或者`git rebase –skip` 忽略冲突

# 说下你对 Reflect 的理解?为什么会有 Reflect 的出现?

# redux-saga 和 mobx 的比较

# 举例说明 React 插槽有哪些应用场景?

# master 挂了的话，pm2 如何处理?

# 上传文件的 content_type 使用什么，node 如何拿到上传的文件内容(不适用第三方插件)，文件内容是一次性传输过去的么?

# 你知道 Vue 的模板语法用的是哪个 web 模板引擎么?说说你对模板引擎的理解?

# 如何实现 Redux 异步功能？

# npm2 和 npm3+ 有什么区别？

# 介绍下 pm2，pm2 依据什么重启服务？

# 说下 React 的 useEffect、useCallback、useMemo

# 用 CSS 实现 div 宽度自适应，宽高保持等比例缩放

# 移动端适配方案具体实现以及对比

# 单元测试如何测试？代码覆盖率如何？

# setTimeout（1）与 setTimeout（2）之间的区别

# JavaScript 里垃圾回收机制是什么？常用的是哪种，怎样处理的？

# 16.X 中 props 改变后在哪个生命周期中处理?

# 简述 Vue 的基本原理

# JS 中如何实现一个类?怎么实例化这个类?

# for…in 和 object.keys 的区别

# 使用原型链如何实现继承?

# 在一个 DOM 上同时绑定两个点击事件：一个用捕获，一个用冒泡。事件会执行几次?先执行的是冒泡还是捕获?

# 说一下 setTimeout 和 setInterval 在内存方面的区别?

# redux 的设计思想

# 301、302 的 https 被挟持怎么办?

# 说说开发中常用的几种 Content-Type?

# 说一下你对进程和线程的了解?

# 说一下什么是 http 协议无状态？怎么解决 http 协议无状态?

# 说一下 JavaScript 严格模式下有哪些不同?

# 说说使用过 koa2 的哪些中间件，其原理是什么?

# 如何配置 React-Router 实现路由切换？

# webpack 如何利用 localStorage 离线缓存静态资源？

# 浏览器缓存了解么?

# 10 个资源放在一个域名下加载和放在多个域名下加载的区别是?

# setTimeout/setInterval 实现倒计时如何解决时间偏差的问题?

# HTTP2.0 的多路复用和 HTTP1.x 中的长连接复用有什么区别？

# node 原生 api 错误处理有了解的么？

# node 中进程间是如何进行通信的?

# 说一下 webpack 中 css-loader 和 style-loader 的区别，file-loader 和 url-loader 的区别？

# 什么是 CSP?

# 使用 Symbol 函数都有哪些要注意的点?

# 深拷贝如何解决循环引用?

# Array 是 Object 类型么?

# 为什么说 React 中 props 是只读的?

# 说一下变量的作用域链

# 如何获取 html 元素实际的样式值?

# vue2.x 为什么要求组件模板只能由一个根元素?

# 说一下你对 get 和 post 请求在缓存方面的理解

# 页面埋点怎么实现?

# 如果我不想让别人对 obj 对象添加或者删除元素，可以怎么做呢?

# Vue 切换路由的时候，需要保存当时状态的功能，怎么实现呢?

# 为什么使用 setTimeout 实现 setInterval?怎么模拟?

# 用 for 模拟实现 forEach

# 如何解决 vue 打包 vendor 过大的问题?webpack 打包 vue 速度慢怎么办?

# 在 map 中和 for 中调用异步函数的区别?

# Reflect.ownKeys 与 Object.keys 的区别

# 除了 jsonp、postmessage 后端控制，怎么实现跨页面通讯?

# 请实现一个 cacheRequest 方法，保证发出多次同一个 ajax 请求时都能拿到的数据，而而实际上只发出一次请求。

# 说说你对 Context 的理解，为什么 React 并不推荐我们优先考虑使用 Context?

# React Hooks 的 useState 相对于有状态组件 state 区别是什么?

# 说一下 etag 和 lastmodify 的区别

# vue Hooks 有哪些

# 强缓存都有哪些方法来控制

# 说一下 vm.$set 原理

# 说一下项目性能优化过程中，是怎样充分利用 chrome 调试工具的?

# 说一下对事件流的理解

# 在 Vue 中父组件可以监听到子组件的生命周期么?

# class 的继承和 prototype 继承 是完全一样的么?

# React Hooks 解决的问题是什么?以 useRffect 为例子说明下其原理是什么?

# HTTPS 怎么建立安全通道，HTTPS 的加密过程

# 说一下你对 Vue 中 keep-alive 的理解，以及在使用过程中需要注意的地方?

# 在 ES6 中有哪些解决异步的方法

# Redux 如何优化

# Prerender 预渲染的原理

# 实现柯里化函数

# React兄弟组件的通信方式

# Generator yield 的作用

# 说出前端框架设计模式(MVVM 或 MVP 或 MVC)的含义以及原理

# 预渲染 prerender-spa-plugin 能详细讲解么

# 请说明JS进行压缩、合并、打包实现的原理是什么?为什么需要压缩、合并、打包

# 手动实现jsonp

# 多个组件之间如何拆分各自的 state，每块小的组件有自己的状态，他们之间还有一些公共的状态需要维护，你会怎么思考

# 说说你所理解的 Redux 数据流的流程

# 封装公共组件需要注意什么

# 使用过 mobx 么?mobx 和 redux 有什么区别?

# ES6 类继承中 super 的作用

# 手写实现 js 中的深拷贝

# 脚手架具体做了哪些事情，webpack 具体做了什么配置?怎样优化包的大小?

# webpack怎样优化包的大小

# 使用原型最大的好处

# setInterval 需要注意的点

# nextTick 是在本次循环执行，还是在下次循环执行呢?setTimeout(()=>{},1000)是怎样执行的呢?

# JS 写一个单例模式，具体的场景

# 请解释下 http 中所有请求方法

# Vue 调用 push 给数组添加元素会自动更新么?原因是什么?

# 说一下网络通信中引入滑动窗口的作用

# 说一下 http2 的特性，http2 怎么确保文件同时传输不会报错?

# JS 是多线程么?绑定一个事件的回调函数是宏任务还是微任务?

# 怎么理解 vue 的单向数据流

# Promise.allSettled 了解么?试着手写下 Promise.allSettled

# Vuex 的 action 和 mutation 的特性是什么?有什么区别?

# 说一下路由钩子在 vue 生命周期的体现

# 什么是 React Hooks?为什么需要 Hooks

# Token 一般是存放在哪里

# redux 和全局管理有什么区别

# React Hooks 实现原理

# Token 放在 cookie 和放在 localStorage、sessionStorage 中有什么不同

# 页面刷新后的vuex的state数据丢失怎么办

# WebSocket 如何断开重连

# 完整的路由导航解析流程(不包括其他生命周期)

# 如何实现按需加载

# Vuex 怎么知道 state 是通过 mutation 修改还是外部直接修改的

# 为什么说利用多个域名来存储网站资源会更有效

# 箭头函数和普通函数的区别

# 请求在客户端报413是什么错误,怎么解决呢

# TypeScript里面有哪些JavaScript没有的类型

# 组件库设计有什么原则呢

# vue 如何做权限校验

# 说一下对 URL 进行编码/解码的实现方式

# 说一下Taro的编译原理

# node 起服务如何保证稳定性

# node 接口转发有无做什么优化

# 说一下 React-redux 的理解以及它的原理，主要是解决了什么问题

# 设计搜索组件(具有自动补全功能组件)，你需要考虑的问题是什么

# 用原生js实现自定义事件

# node如何平缓降级，重启

# 说一下 redux 的原理，介绍下整体的工作流程

# node 的适用场景以及优缺点是什么

# 说一下get、post、put的区别

# 介绍下 npm 模块安装机制?输入 npm install 命令敲下回车后它的执行流程是什么?

# umi 是干什么用的?其优缺点是?

# 说一下对 ESLint 的了解? 如何使用? 它的工作原理?

# PWA 是什么,对 PWA 有什么了解

# webpack打包出来的体积太大，如何优化体积?

# 对 to B 和 to C 的业务的理解

# setTimeout 有什么缺点，和 requestAnimationFrame 有什么区别

# dva 是干什么用的?其优缺点是?

# 是否了解 glob 库，glob 是如何处理文件的?是否有别的方法

# 说一下面向对象的理解，面向对象有什么好处

# 如何做工程上的优化

# 描述下自定义指令(vue部分)

# position 定位有什么属性

# meta 元素都有什么

# 什么是功能检测、功能推断、UA 字符串

# 鼠标滚动的时候，会触发很多次事件，你是如何解决的

# get请求传参长度存在限制，是http协议限制的么

# 说一下 vuex 的原理以及自己的理解

# state 是怎样注入到组件的，从 redux 到组件经历了什么样的过程

# 定时器为什么是不精确的

# 搜索请求如何处理?搜索请求中文如何处理?

# prototype 和 proto 区别

# 接入 Redux 过程?绑定 connect 的过程?connect 的原理是什么

# 说一下对 BigInt 的理解,在什么场景下会使用

# 说说浏览器渲染流程，分层之后在什么时候合成

# 说一下进程和线程的区别

# 了解 CSS 模块吗

# Redux 中间件是什么东西?接收几个参数?柯里化函数两端的参数具体是什么东西

# React 异步渲染的概念，请介绍 Time Slicing 和 Suspense

# 怎样避免重排，重绘

# 什么是重排，重绘

# 为什么要用 vuex 或者 Redux

# 介绍 immutable

# React 如何避免 render 的触发

# 说下在项目开发,你是怎样组织 CSS 的

# 解决跨域都有哪些手段

# 说说你理解的懒加载的理解

# React 项目中有哪些细节可以优化?实际开发中都做过哪些性能优化?

# 简单描述静态链接和动态链接的区别，并举例说明

# 请实现一个 JSON.stringify

# 说说你对图片的预加载的理解

# DNS 解析的具体过程

# JavaScript 中如何模拟实现方法的重载

# 异步请求，低版本 fetch 如何低版本适配

# 对 React 的看法是什么?它的优缺点是什么?使用过程中遇到的问题是如何解决的?

# 一个 dom 必须要操作几百次，改如何解决，如何优化?

# redux 请求中间件如何处理并发

# 给出页面的加载顺序

# 什么是死锁

# utf-8 和 asc 码有什么区别

# 如何创建一个 ajax

# vue的双向绑定的原理是什么？

# Loader和Plugin的区别是什么？

【Loader】：用于对模块源码的转换，loader描述了webpack如何处理非javascript模块，并且在buld中引入这些依赖。loader可以将文件从不同的语言（如TypeScript）转换为JavaScript，或者将内联图像转换为data URL。比如说：CSS-Loader，Style-Loader等。

loader的使用很简单：

在webpack.config.js中指定loader。module.rules可以指定多个loader，对项目中的各个loader有个全局概览。

loader是运行在NodeJS中，可以用options对象进行配置。plugin可以为loader带来更多特性。loader可以进行压缩，打包，语言翻译等等。

loader从模板路径解析，npm install node_modules。也可以自定义loader，命名XXX-loader。

语言类的处理器loader：CoffeeScript，TypeScript，ESNext（Bable）,Sass,Less,Stylus。任何开发技术栈都可以使用webpack。

【Plugin】：目的在于解决loader无法实现的其他事，从打包优化和压缩，到重新定义环境变量，功能强大到可以用来处理各种各样的任务。webpack提供了很多开箱即用的插件：CommonChunkPlugin主要用于提取第三方库和公共模块，避免首屏加载的bundle文件，或者按需加载的bundle文件体积过大，导致加载时间过长，是一把优化的利器。而在多页面应用中，更是能够为每个页面间的应用程序共享代码创建bundle。

webpack功能强大，难点在于它的配置文件，webpack4默认不需要配置文件，可以通过mode选项为webpack指定了一些默认的配置，mode分为：development/production，默认是production。

插件可以携带参数，所以在plugins属性传入new实例。

# 请解释React中props和state的区别？

在React中props和state都属于组件的数据，他们的改变都可能会触发组件的重新渲染。 

- props 是组件对外的接口，对于传入的组件而言时可读的、不可变的，遵循单向数据流原则

- state 是维护组件内部状态的， 是可变的。 

组件内可以引用其他组件，组件之间的引用形成了一个树状结构，如果下层组件需要使用上层组件的数据或方法，上层组件就可以通过下层组件的props属性进行传递，因此props是组件对外的接口，用于组件间的通信。props不能通过子组件自身的方法修改，只能通过父组件传递的回调函数在父组件进行修改。 组件除了使用上层组件传递的数据外，自身也可能需要维护管理数据，这就是组件对内的接口state。修改组件内部状态需要使用setState或forceUpdate方法来改变。 根据对外接口props 和对内接口state，组件计算出对应界面的UI。 

主要区别： 
- state是可变的，是一组用于反映组件UI变化的状态集合；
- props对于使用它的组件来说，是只读的，要想修改props，只能通过该组件的父组件修改。 在组件状态提升的场景中，父组件正是通过子组件的props, 传递给子组件其所需要的状态。
- 没有state的组件叫做无状态组件，它接收props，只负责渲染，反之则叫做有状态组件。工作中应尽量使用无状态组件，增加代码的可维护性和复用性。

# 浏览器的本地存储(1)的cookie了解多少？

HTTP Cookie（也叫 Web Cookie 或浏览器 Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。通常，它用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。Cookie 使基于无状态的HTTP协议记录稳定的状态信息成为了可能。 

Cookie 主要用于以下三个方面： 

- 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息） 

- 个性化设置（如用户自定义设置、主题等） 

- 浏览器行为跟踪（如跟踪分析用户行为等） 

Cookie 的生命周期可以通过两种方式定义：

- 会话期 Cookie 是最简单的 Cookie：浏览器关闭之后它会被自动删除，也就是说它仅在会话期内有效。会话期Cookie不需要指定过期时间（Expires）或者有效期（Max-Age）。需要注意的是，有些浏览器提供了会话恢复功能，这种情况下即使关闭了浏览器，会话期Cookie 也会被保留下来，就好像浏览器从来没有关闭一样，这会导致 Cookie 的生命周期无限期延长。 

- 持久性 Cookie 的生命周期取决于过期时间（Expires）或有效期（Max-Age）指定的一段时间。

# 浏览器的本地存储(2)的WebStorage了解多少？

# 说一下vue-router的原理是什么?

# 防抖节流原理、区别以及应用，请用js实现。

# 在css中link和@import的区别是什么？

首先，他们本质都是为了加载css文件。

### link
```
<link href="css 路径" rel="stylesheet" type="text/css" />
```

### @import
```
@import url(css 文件路径地址);
```

### 区别

语法结构不同，如上所示：
- link是html标签，只能放到html文档中使用
- @import是css提供的一种引入样式的方式，因此需要放在<style type="text/css">标签中
- 
用途不同：
- link标签除了加载css文件外，还可以定义RSS，定义rel链接属性登
- @import只能加载css

加载顺序不同：
- 当一个页面被加载的时候，link引用的css会同时被加载
- @import引用的css则会等到页面完全被下载完才会去加载，因此，浏览@import加载css的页面时会没有样式（闪烁）

兼容：
- @import在老浏览器中不支持

总结：推荐link方式

# 常见的loader以及作用的总结

Loader用于对模块的源代码进行转换，可以使你在 import 或 加载模块时预处理文件。由于webpack本身只能打包JavaScript文件，对于其他资源，如css、图片、JSX等是无法处理的。这时候就需要用到loader将资源转化。Loader本质上就是一个export出来的函数，接受要处理的源文件字符串，返回经过“翻译”后的webpack可以直接处理的模块。

常用loader及作用：
- raw-loader：加载文件原始内容（utf-8）
- file-loader：把文件输出到一个文件夹中，在代码中通过相对URL去引用输出的文件
- url-loader：和file-loader类似，但是能在文件很小的情况下以base64的方式把文件内容注入到代码中
- source-map-loader：加载额外的Source Map文件，以方便断点调试
- svg-inline-loader：将压缩后的 SVG 内容注入代码中
- image-loader：加载并且压缩图片文件
- json-loader：加载 JSON 文件（默认包含）
- handlebars-loader：将 Handlebars 模版编译成函数并返回
- babel-loader：把ES6转化成ES5
- ts-loader: 将 TypeScript 转换成 JavaScript
- awesome-typescript-loader：将 TypeScript 转换成 JavaScript，性能优于 ts-loader
- css-loader：加载css，支持模块化、压缩、文件导入等特性
- style-loader：把css代码注入到js中，通过DOM操作去加载css
- eslint-loader：通过ESLint检查JS代码
- tslint-loader：通过 TSLint检查 TypeScript 代码
- postcss-loader：扩展 CSS 语法，使用下一代 CSS，可以配合 autoprefixer 插件自动补齐 CSS3 前缀
- vue-loader：加载 Vue.js 单文件组件
- cache-loader: 可以在一些性能开销较大的 Loader 之前添加，目的是将结果缓存到磁盘里

# vue计算属性和普通属性的区别是什么?

# webpack中source map是什么？生产环境怎么用？

# 浏览器缓存机制(1)对于开发很重要，强缓存的内容能了解多少呢？

# 介绍js全部数据类型，基本数据类型和引用数据类型的区别

# react-router里的Link标签和a标签有什么区别？

# 说一说XSS攻击

# 谈谈你对重绘和回流的理解

# 简单说下你理解的语义化，怎样来保证你写的符合语义化？HTML5语义化标签了解下

# 常见的plugin以及作用的总结

# 说一下关于tree-shaking的原理

# 如何实现 webpack 持久化缓存

# webpack的构建流程是什么

# 说一说CSRF攻击

# CSS伪类和伪元素区别

### 什么是css伪类（CSS pseudo-classes）
伪类的概念引入是为了能够表达在文档树语法之外无法通过简单的选择器表达的信息。伪类的语法是单个冒号带一个伪类名称。不区分大小写。有的伪类是互斥的，有的可以同时作用在同一个元素上，伪类也可以是动态的，来响应用户的交互。

有哪些伪类：
- :link 默认带href属性的a标签的样式
- :visited 被访问过的链接的样式
- :hover 鼠标悬浮上去的样式
- :active 鼠标按下去的时候的样式
>（上面四种定义的时候需要保证这样的顺序）

- :focus 当前元素为focus状态
- :lang lang(en) 对应html上的lang属性，符合的话执行样式
- :empty 选择没有子元素的元素执行样式
- :enable 选择表单元素具有非disable属性的元素，执行样式
- :disable 选择表单元素具有disable属性的元素。执行样式
- :checked 单选按钮或者多选按钮被选中的，执行样式
- :target 锚点跳转到的内容执行样式
- :root 匹配文档的根元素。html中默认就是html元素
- :default 默认状态的表单元素，比如默认选中的下拉框，单选按钮，多选按钮，执行样式
- :first-of-type 选中该元素是别人首个子元素，例如p:first-of-type 就是所以元素子元素中第一个p元素
- :last-of-type 意义和上面类似，代表最后一个
- :only-of-type 代表所有元素中只有一个该类型的元素p:only-of-type
- :only-child 例如p:only-child 代表子元素中只有一个元素，且必须是该类型p
- :first-child 例如p:first-child 代表是父元素中的第一个元素，且类型为p
- :last-child 意义同上，最后一个元素
- :nth-child(n) 例如p:nth-child(2) 表示选择子元素第二个且类型为p的元素，n从1开始算
- :nth-last-child(n) 意思和上面类似，只不过是从结尾开始往前数第n个，n是从1开始算
- :nth-of-type(n) 例如p:nth-of-type(2) 代表子元素中第二次出现的p元素 n从1开始算
- :nth-last-of-type(n) 意义和上面类似，只不过是从尾部往前数，n从1开始算
- :not() 例如 :not(p) 匹配非p元素

### 什么是css伪元素（CSS pseudo-element）
伪元素是在html文档树语法的基础上创造的一种抽象概念，例如，文档树语法里并没有提供一种机制让我们访问一个元素的内容的首个字母或者首行，伪元素提供了访问这样难以访问的信息的能力，伪元素还提供了对dom节点内不存在的内容的引用和生成能力，比如::after ::before 提供了生成内容的能力。

一个伪元素包含两个冒号 ::

有哪些常用伪元素：
- ::first-letter 匹配内容的首个字符
- ::first-line 匹配内容的首行内容
- ::before 匹配内容前面的部分
- ::after 匹配紧跟内容后面的部分
- ::selection 匹配用户通过鼠标或者其他设备选中的内容部分

### 伪类和伪元素的区别

1、写法的区别

在css3中定义了双冒号代表伪元素，单冒号代表伪类。以此来区分伪元素和伪类。为了兼容老的浏览器，用单冒号类表达伪元素也是能够被识别的，比如写:after :before :first-line :fist-letter。

2、概念的区别

伪类侧重丰富选择器的选择语法范围内元素的选择能力，伪元素侧重表达或者定义不在语法定义范围内的抽象元素。

3、兼容性

伪类和伪元素各自有一些存在的兼容问题。

# Vuex和localStorage的区别

# 说一下事件循环机制(node 浏览器)

# webpack的构建流程是什么

# Import和CommonJs在webpack打包过程中有什么不同

# dev-server是怎么跑起来的

# 谈谈关于对webpack热更新的原理

# 浏览器缓存机制(3)对于开发很重要，缓存位置的内容能了解多少呢

# webpack打包时Hash码是怎样生成的？随机值存在一样的情况，如何避免？

# 如何加快页面渲染速度，都有哪些方式？(js方面)

# HTTP请求特征是什么

# react里组件通信有几种方式，分别怎样进行通信

# 说一下栈和堆的区别，垃圾回收时栈和堆的区别

# 布局都有什么方式，float和position有什么区别

# 用JS代码实现事件代理

# 对虚拟DOM的理解？虚拟DOM主要做了什么？虚拟DOM本身是什么？

# 移动端需要注意什么

# 响应式布局用到的技术有几种方式

# 词法作用域和this的区别

# 介绍React高阶组件，适用于什么场景？

# 说一下Vue的keep-alive是如何实现的，具体缓存的是什么

# 请描述下css盒模型基本概念

# React组件中怎么做事件代理？它的原理是什么？

# Promise 构造函数是同步还是异步执行，then呢？

# 说一下mobx和redux有什么区别

# CSS预处理器的概念

# shouldComponentUpdate是为了解决什么问题

# React里setState到底是异步还是同步

# react-redux的工作流程是什么

# 添加原生事件不移除为什么会内存泄漏，还有哪些地方会存在内存泄漏？（js）

# 怎么处理项目中的异常捕获行为

# 点击一个按钮，浏览器会做些什么事情【呈现效果时流程】

# 解决异步的问题的几种方式？Promise解决了异步问题吗？

# 与HTTP相关的协议有哪些？TCP/IP DNS URI/URL HTTPS

# CDN有哪些优化静态资源加载速度的机制

# 说说你理解的node 中间层怎样做的请求合并转发

# webpack做了什么？使用webpack构建是否有做一些自定义操作

# webpack如何用localStorage离线缓存静态资源

# 关于对 Vue 项目进行优化有哪些？

# 说一下React.Component和React.PureComponent的区别

# 使用import时，webpack对node_modules里的依赖会做什么

# Redux和Vuex有什么区别,说一下它们的共同思想

# 为什么组件中的 data 必须是一个函数，然后 return 一个对象，而 new Vue 实例里，data 可以直接是一个对象

# 说一下mysql和mongodb的区别

# 说一下你对React context的理解

# webpack 里面的插件是如何实现的

# 使用TS的优势有哪些

# 直接给一个数组项赋值，Vue 能检测到变化吗

# Vue 组件间通信有哪几种方式

# 项目如何管理模块

# 在哪个生命周期内调用异步请求

# 说明一下JS封装的原理

# 说出常用的页面优化实现方案

# 回调函数和任务队列的区别

# 请你谈谈对无状态的理解 (React)

# 如何理解事件委托

# BFC是什么？触发BFC的条件是什么？有哪些应用场景

# 说一下单向数流有什么好处

# React怎么做数据检查和变化

# 类数组转化为数组

# 说一下关于tree-shaking的原理

# Vue 中的 key 有什么作用

# 说一下Vue 的父组件和子组件生命周期钩子函数执行顺序

# 使用过 Vue SSR 吗？说说 SSR

# 什么情况下出现浏览器分层？(css部分)

# 说下JS继承的原理

# 说一下Vue的$nextTick原理

# 说一下Vue单页与多页的区别

# v-model是如何实现的，语法糖实际是什么

# 怎样理解 Vue 的单向数据流

# React SSR实现过程

# React SSR实现原理是什么,需要注意什么事项

# 子组件可以直接改变父组件的数据么？说说你的理由？(vue)

# 能说下 vue-router 中常用的 hash 和 history 路由模式实现原理吗

# 实现数组去重

# 描述下JS中Prototype的概念

# 实现数组扁平化

# React事件绑定原理是什么

# 为什么不建议使用通配符初始化css样式

# 说一下koa2和express区别

# link 标签定义

# 渲染过程中遇到JS文件怎么处理?(浏览器解析过程)

# Object.is()与原来的比较操作符 "===" 、"==" 的区别

使用双等号进行相等判断时，如果两边的类型不一致，则会进行强制类型转化后再进行比较

使用三等号进行相等判断时，如果两边的类型不一致时，不会做强制类型准换，直接返回 false

使用 Object.is 来进行相等判断时，一般情况下和三等号的判断相同，它处理了一些特殊的情况，比如 -0 和 +0 不再相等，两个 NaN 认定为是相等的。

# 三种事件模型是什么

1、DOM0级事件模型（原始事件模型）

通过属性绑定，如 onclick="xxxx()"，或者通过获取到元素后，以赋值的形式绑定事件

2、DOM2级事件模型

新增了捕获和冒泡机制，并支持同一个元素绑定多个事件。

DOM2 级事件模型共有三个阶段：

事件捕获阶段：事件从 document 向下传播到目标元素，依次检查所有节点是否绑定了监听事件，如果有则执行。

事件处理阶段：事件在达到目标元素时，触发监听事件。

事件冒泡阶段：事件从目标元素冒泡到 document，并且一次检查各个节点是否绑定了监听函数，如果有则执行。

3、IE事件模型

IE事件只支持冒泡，所以事件流有两个阶段：

事件处理阶段：事件在达到目标元素时，触发监听事件。

事件冒泡阶段：事件从目标元素冒泡到 document，并且一次检查各个节点是否绑定了监听函数，如果有则执行。


# DOCTYPE 的作用是什么

# iframe有哪些缺点

# 说说你对浏览器的理解

# 谈谈你对ajax的理解

# 简单介绍使用图片base64编码的优点和缺点

# 请说出目前主流的js模块化实现的技术有哪些?他们的区别在哪儿

# for..in和Object.keys的区别
for..in
- 遍历对象上及其原型链上可枚举的属性
- 如果用于遍历数组，除了遍历其元素外，还会遍历开发者对数组对象自定义的可枚举属性及其原型链上的可枚举属性（不推荐for...in遍历数组)
- 遍历对象返回的属性名和遍历数组返回的索引都是字符串类型
- 某些情况下，可能按随机顺序遍历数组元素

Object.keys
- 返回对象自身可枚举属性组成的数组
- 不会遍历对象原型链上的属性以及Symbol属性
- 对数组的遍历循序和for..in一致

for of
- es6中添加的循环遍历语法
- 支持遍历数组，类数组对象(DOM NodeList)，字符串，Map对象，Set对象
- 不支持遍历普通对象
- 遍历后输出的结果为数组元素的值
- 可搭配实例方法entries(),同时输出数组的内容和索引

# 哪些操作会造成内存泄漏

# 什么是浏览器的同源策略

# 说一下你理解margin重叠的问题

# 网页验证码是干嘛的，是为了解决什么安全问题

# display、position和float的相互关系

# 前端需要注意哪些SEO

SEO具体是指通过网站结构调整、网站内容建设、网站代码优化、以及站外优化（网站站外推广、网站品牌建设等），使网站满足搜索引擎的收录排名需求，提高网站在搜索引擎中关键字的排名，从而吸引精准用户进入网站，获得免费流量，产生直接销售或品牌推广。

需要注意：

1、 合理的title，description，keyswords 搜索引擎对这三项的权重逐个减小，title 值强调重点即可，重要的关键

词出现不要超过两次，而且要靠前。

2 、不同页面的tilte要有所不同；description把页面的内容高度概括，长度合适，不可过分堆叠关键词，不同页面

description有所不同。keyswords列举出重要的关键词即可。

3、语义化的HTML代码，符合W3C 规范：语义化代码有利于搜索引擎理解网页。

4 、重要的内容HTML代码放在前面：搜索引擎抓取HTML 的顺序是从上到下，有的搜索引擎对抓取长度有限制，保

证重要内容一定会被抓取。

5 、重要的内容不要用js输出，爬虫不会执行js获取内容。

6 、尽量少用iframe ，搜索引擎不会抓取iframe中的内容。

7 、非装饰的图片必须加alt 。

8 、提高网站速度：网站速度是搜索引擎排序的一个重要指标。

# 简单说一下V8引擎的垃圾回收机制

# 谈谈对JSON的理解

# 渲染页面时常见的不良现象有哪些?(浏览器渲染过程)
白屏、闪烁

# html布局元素的分类有哪些? 描述下每种布局元素的应用场景

# componentWillReceiveProps的触发条件是什么

# javascript 代码中的"use strict"是什么意思?为什么使用它 

# javascript 代码中的"use strict"是什么意思?为什么使用它

# 什么是 polyfill

# 说一下Vue的生命周期以及每个阶段做的事情
1.beforeCreate(创建前) 在数据观测和初始化事件还没有开始

2.created(创建后) 完成数据观测，属性和方法的运算，初始化事件，$el属性还没有显示出来

3.beforeMounted(挂载前) 在挂载开始之前被调用，相关的render函数首次被调用。实例已完成下面的配置：编译模板，把data里面的数据和模板生成html。此时还没有挂载html到页面上

4.mounted(挂载后) 在el被新创建的vm.$el替换，并挂载到实例上去之后调用。实例已经完成下面的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html页面中，此过程中可进行ajax交互

5.beforeUpdate(更新前) 在数据更新之前调用，发生在虚拟dom重新渲染和打补丁之前。可以在该钩子中进一步更改状态，不会触发重复渲染过程

6.update(更新后) 在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用时，组件dom已经更新，所以可以执行依赖于dom操作。但是在大多数情况下，在此期间避免更改状态，因为这可能会导致更新无法循环。此钩子在服务端渲染期间不被调用

7.beforeDestroy(销毁前) 在实例销毁之前调用。实例仍然完全可以用。

8.destroyed(销毁后) 在实例销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实例也会被销毁。此钩子在服务端渲染期间不被调用

# 你所理解的同步和异步的区别是什么

# javascript 创建对象的几种方式

# 说一下你所理解JavaScript中的作用域与变量声明提升

# 内部属性[[Class]]是什么

# 检测浏览器版本版本有哪些方式

# React 高阶组件、Render props和hooks有什么区别,为什么不断迭代

# 说一下Vue template到render的过程

# 如何解决跨域问题

- 将 document.domain 设置为主域名，来实现相同子域名的跨域操作，这个时候主域名下的 cookie 就能够被子域名所访问。同时如果文档中含有主域名相同，子域名不同的 iframe的话，我们也可以对这个 iframe 进行操作。如果是想要解决不同跨域窗口间的通信问题，比如说一个页面想要和页面的中的不同源的iframe 进行通信的问题，我们可以使用 location.hash 或者 window.name 或者postMessage 来解决问题

- 使用 location.hash 的方法，我们可以在主页面动态的修改 iframe 窗口的 hash 值，然后在 iframe 窗口里实现监听函数来实现这样一个单向的通信。因为在 iframe 是没有办法访问到不同源的父级窗口的，所以我们不能直接修改父级窗口的 hash 值来实现通信，我们可以在 iframe 中再加入一个 iframe ，这个 iframe 的内容是和父级页面同源的，所以我们可以 window.parent.parent 来修改最顶级页面的 src，以此来实现双向通信。

- 使用 window.name 的方法，主要是基于同一个窗口中设置了 window.name 后不同源的页面也可以访问，所以不同源的子页面可以首先在 window.name 中写入数据，然后跳转到一个和父级同源的页面。这个时候级页面就可以访问同源的子页面中 window.name 中的数据了，这种方式的好处是可以传输的数据量大。

- 使用 postMessage 来解决的方法，这是一个 h5 中新增的一个 api。通过它我们可以实现多窗口间的信息传递，通过获取到指定窗口的引用，然后调用 postMessage 来发送信息，在窗口中我们通过对 message 信息的监听来接收信息，以此来实现不同源间的信息交换。如果是像解决 ajax 无法提交跨域请求的问题，我们可以使用 jsonp、cors、websocket 协议、服务器代理来解决问题。

- 使用 jsonp 来实现跨域请求，它的主要原理是通过动态构建 script 标签来实现跨域请求，因为浏览器对 script 标签的引入没有跨域的访问限制 。通过在请求的 url 后指定一个回调函数，然后服务器在返回数据的时候，构建一个 json 数据的包装，这个包装就是回调函数，然后返回给前端，前端接收到数据后，因为请求的是脚本文件，所以会直接执行，这样我们先前定义好的回调函数就可以被调用，从而实现了跨域请求的处理。这种方式只能用于 get请求。

- 使用 CORS 的方式，CORS 是一个 W3C 标准，全称是"跨域资源共享"。CORS 需要浏览器和服务器同时支持。目前，所有浏览器都支持该功能，因此我们只需要在服务器端配置就行。浏览器将 CORS 请求分成两类：简单请求和非简单请求。对于简单请求，浏览器直接发出 CORS 请求。具体来说，就是会在头信息之中，增加一个 Origin 字段。Origin 字段用来说明本次请求来自哪个源。服务器根据这个值，决定是否同意这次请求。对于如果 Origin 指定的源，不在许可范围内，服务器会返回一个正常的 HTTP 回应。浏览器发现，这个回应的头信息没有包含Access-Control-Allow-Origin 字段，就知道出错了，从而抛出一个错误，ajax 不会收到响应信息。如果成功的话会包含一些以 Access-Control- 开头的字段。非简单请求，浏览器会先发出一次预检请求，来判断该域名是否在服务器的白名单中，如果收到肯定回复后才会发起请求。

- 使用 websocket 协议，这个协议没有同源限制。

- 使用服务器来代理跨域的访问请求，就是有跨域的请求操作时发送请求给后端，让后端代为请求，然后最后将获取的结果发返回。

# margin和padding分别适合什么场景使用

# CSS多列等高如何实现

# 如何处理HTML5新标签的浏览器兼容问题

# 介绍一下你对浏览器内核的理解

# 扫描二维码登录网页是什么原理，前后两个事件是如何联系的

# 说一下你所理解的渲染原理

- 首先解析收到的文档，根据文档定义构建一棵 DOM 树，DOM 树是由 DOM 元素及属性节点组成的。

- 然后对 CSS 进行解析，生成 CSSOM 规则树。

- 根据 DOM 树和 CSSOM 规则树构建渲染树。渲染树的节点被称为渲染对象，渲染对象是一个包含有颜色和大小等属性的矩形，渲染对象和 DOM 元素相对应，但这种对应关系不是一对一的，不可见的 DOM 元素不会被插入渲染树。还有一些 DOM 元素对应几个可见对象，它们一般是一些具有复杂结构的元素，无法用一个矩形来描述。

- 当渲染对象被创建并添加到树中，它们并没有位置和大小，所以当浏览器生成渲染树以后，就会根据渲染树来进行布局（也可以叫做回流）。这阶段浏览器要做的事情是要弄清楚各个节点在页面中的确切位置和大小。通常这一行为也被称为“自动重排”。

- 布局阶段结束后是绘制阶段，遍历渲染树并调用渲染对象的 paint 方法将它们的内容显示在屏幕上，绘制使用 UI 基础组件。值得注意的是，这个过程是逐步完成的，为了更好的用户体验，渲染引擎将会尽可能早的将内容呈现到屏幕上，并不会等到所有的 html都解析完成之后再去构建和布局 render 树。它是解析完一部分内容就显示一部分内容，同时，可能还在通过网络下载其余内容。

# 如何判断一个对象是否属于某个类

- 第一种方式是使用 instanceof 运算符来判断构造函数的 prototype 属性是否出现在对象的原型链中的任何位置

- 第二种方式可以通过对象的 constructor 属性来判断，对象的 constructor 属性指向该对象的构造函数，但是这种方式不是很安全，因为 constructor 属性可以被改写

- 第三种方式，如果需要判断的是某个内置的引用类型的话，可以使用Object.prototype.toString.call() 方法来打印对象的[[Class]] 属性来进行判断

# 什么是DOM和BOM

# CSS选择符有哪些
id 选择器（#myid）

类选择器（.myclassname）

标签选择器（div,h1,p）

后代选择器（h1 p）

相邻后代选择器（子）选择器（ul>li）

兄弟选择器（li~a）

相邻兄弟选择器（li+a）

属性选择器（a[rel="external"]）

伪类选择器（a:hover,li:nth-child）

伪元素选择器（::before、::after）

通配符选择器（*）

# 标准模式与兼容模式各有什么区别

# css如何影响文档解析

css加载不会阻塞DOM树的解析, 但会阻塞DOM树的渲染，也会阻塞后面js语句的执行。 因此，为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以下几种方法:

1、使用CDN(因为CDN会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)

2、对css进行压缩(可以用很多打包工具，比如webpack,gulp等，也可以通过开启gzip压缩)

3、合理的使用缓存(设置cache-control,expires,以及E-tag都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决防范是在文件名字后面加一个版本号)

4、减少http请求数，将多个css文件合并，或者是干脆直接写成内联样式(内联样式的一个缺点就是不能缓存)

# 说一下你所了解的javascript的作用域链

# DOMContentLoaded事件和Load事件的区别

# Symbol 值的强制类型转换

# HTML5有哪些新特性、移除了哪些元素

HTML5新特性：

拖放（Drag and drop）API

语义化标签（header、nav、footer、section、article、aside）

音频、视频（audio、video）API

画布（canvas）API

地理定位（Geolocation）API

本地离线存储（localStorage），即长期存储数据，浏览器关闭后数据不丢失；会话存储（sessionStorage），即数据在浏览器关闭后自动删除

表单控件（calender、date、time、url、email、search）

新的技术（webworker、websocket）

新的文档属性 document.visibilityState


移除的元素：

纯表现的元素：basefont、big、center、font、s、strike、tt、u

对可用性产生负面影响的元素：frame、frameset、noframes

# 说一下对DTD的理解

DTD（ Document Type Definition 文档类型定义）是一组机器可读的规则，它们定义 XML或 HTML 的特定版本中所有允许元素及它们的属性和层次关系的定义。在解析网页时，浏览器将使用这些规则检查页面的有效性并且采取相应的措施。

DTD 是对 HTML 文档的声明，还会影响浏览器的渲染模式（工作模式）。主要用来解决传输问题，它的存在可以使我们能够使用某个标准的DTD来 交换数据、检验数据。

# 常见浏览器所用的内核

- IE 浏览器内核：Trident 内核，也是俗称的 IE 内核

- Chrome 浏览器内核：统称为 Chromium 内核或 Chrome 内核，以前是 Webkit内核，现在是 Blink 内核

- Firefox 浏览器内核：Gecko 内核，俗称 Firefox 内核

- Safari 浏览器内核：Webkit 内核

- Opera 浏览器内核：最初是自己的 Presto 内核，后来加入谷歌大军，从 Webkit又到了 Blink 内核

- 360 浏览器、猎豹浏览器内核：IE + Chrome 双内核

- 搜狗、遨游、QQ 浏览器内核：Trident（兼容模式）+ Webkit（高速模式）

- 百度浏览器、世界之窗内核：IE 内核

- 2345 浏览器内核：好像以前是 IE 内核，现在也是 IE + Chrome 双内核了

- UC 浏览器内核：这个众口不一，UC 说是他们自己研发的 U3 内核，但好像还是基于 Webkit 和 Trident ，还有说是基于火狐内核

# 什么是文档的预解析

# js继承的几种实现方式

# React key是干什么用的,为什么要加上key

key是React用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识

在开发过程中，我们需要保证某个元素的key在其同级元素中具有唯一性

在React Diff算法中React会借助元素的key值来判断该元素是新创建的还是被移动而来的元素，从而减少不必要的元素重新渲染

此外，React还需要借助Key值来判断元素与状态的关联关系

几点注意事项:
- key值一定要和具体的元素一一对应
- 尽量不要使用数组的index去作为key值
- 永远不要试图在render的时候用随机数或者其他操作给元素加上不稳定的key，这样会造成的性能开销比不加key的情况下要糟糕

# 说一下你理解的 HTTPS 中间人攻击

HTPPS 协议由 HTTP + SSL 协议构成

中间人攻击过程如下：

- 服务器向客户端发送公钥

- 攻击者截获公钥，保留在自己手上

- 然后攻击者自己生成一个【伪造的】公钥，发给客户端

- 客户端收到伪造的公钥后，生成加密 hash（秘钥） 值发给服务器

- 攻击者获得加密 hash 值，用自己的私钥解密获得真秘钥

- 同时生成假的加密 hash 值，发给服务器

- 服务器用私钥解密获得假秘钥

- 服务器用假秘钥加密传输信息

防范方法：

服务器在发送浏览器的公钥中加入 CA 证书，浏览器可以验证 CA 证书的有效性；（现有 HTTPS 很难被劫持，除非信任了劫持者的 CA 证书）。

# 说一下你所理解的观察者模式

# SGML、HTML、XML和XHTML的区别

SGML 是标准通用标记语言，是一种定义电子文档结构和描述其内容的国际标准语言，是所有电子文档标记语言的起源

HTML 是超文本标记语言，主要是用于规定怎么显示网页

XML 是可扩展标记语言是未来网页语言的发展方向，XML 和 HTML 的最大区别就在于XML 的标签是可以自己创建的，数量无限多，而 HTML 的标签都是固定的而且数量有限

XHTML 也是现在基本上所有网页都在用的标记语言，他其实和 HTML 没什么本质的区别，标签都一样，用法也都一样，就是比 HTML 更严格，比如标签必须都用小写，标签都必须有闭合标签等

# 说一下你所了解的react-fiber

fiber实现了自己的组件调用栈，它以链表的形式遍历组件树，可以灵活的暂停、继续和丢弃执行的任务。实现方式是使用了浏览器的requestldeCallback这一个api。fiber其实值得是一种数据结构，它可以用一个纯js对象来进行表示。

react内部运转分三层：

- Virtual DOM层：描述页面长什么样子
- Reconciler层:负责调用组件声明周期方法，进行Diff运算等
- Renderer层:根据不同的平台，渲染出相应的页面，常见的是react-dom

为了实现不卡顿的效果，需要有一个调度器(Scheduler)来进行分配。优先级高的任务(键盘输入)可以打断优先级低的任务(diff)的执行，从而更快的生效。任务的优先级有六种：

- synchronous，与之前的Stack Reconciler操作一样，同步执行
- task，在next tick之前执行
- animation，下一帧之前执行
- high，在不久的将来执行
- low，稍微延迟执行也没关系
- offscreen，下一次render时或scroll时才执行

Fiber Reconclier(react)执行阶段:

- 阶段1：生成一个Fiber树，得出需要更新的节点信息。这一步是一个渐进的过程，可以被打断
- 阶段2：将需要更新的节点一次批量更新，这个过程不能被打断。

Fiber树：Fiber Reconciler在阶段1进行diff计算的时候，会基于virtual DOM树生成一颗Fiber树，它的本质是链表。

# 异步编程的实现方式是什么

1、回调函数

优点：简单、容易理解 缺点：不利于维护，代码耦合高，多个异步操作下容易形成回调地狱。

2、Promise

优点：可以利用then方法，进行链式写法；可以书写错误时的回调函数； 缺点：编写和理解，相对比较难，语义不是那么明确

3、Generation

优点：函数体内外的数据交换、错误处理机制 缺点：流程管理不方便，控制权的转换需要特别注意

4、async/await

优点：内置执行器、更好的语义、更广的适用性、返回的是Promise、结构清晰。 缺点：错误处理机制， 需要try-catch捕获

# 什么是函数柯里化

把接收多个参数的函数变换为接收一个单一参数（最初函数的第一个参数）的函数，并返回接收剩余参数而且返回结果的新函数的技术。

优点：

- 可以延迟计算，即如果调用柯里化函数传入参数是不调用的，会将参数添加到数组中存储，等到没有参数传入的时候进行调用

- 参数复用，当在多次调用同一个函数，并且传递的参数绝大多数是相同的，那么该函数可能是一个很好的柯里化函数

# 说一下import的原理，和require的不同之处

import原理(实际上就是ES6 module的原理)：简单来说就是闭包作用。

为了创建Module的内部作用域，会调用一个包装函数

包装函数的返回值也就是Module向外公开的API，也就是所有export出去的变量

import是拿到module导出变量的引用

与require的不同之处：

CommonJS模块输出的是一个值的拷贝，ES6模块输出的值的引用

CommonJS模块是运行时加载，ES6模块是编译时输出接口

CommonJS是运行时加载对应模块，一旦输出一个值，即使模块内部对其做出改变，也不影响输出值。而ES6模块不同，import导入是在JS引擎对脚步静态分析时确定，获取到的是一个只读引用。等脚本引擎运行时，会根据这个引用去对应模块中的取值，所以引用对应的值改变的时候，其导入的值也会发生改变

# 使用 Object.defineProperty() 来进行数据劫持有什么缺点

1、无法检测到对象属性的新增或删除

2、无法监听数组变化

替代方案： ES6 Proxy

# 面向对象的三要素是什么，分别是什么意思

封装: 把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏

继承: 使用现有类的所有功能并在无需重新编写原来的类的情况下对这些功能进行扩展

多态: 一个类实例的相同方法在不同情形下有不同表现形式。多态机制使具有不同内部结构的对象可以共享相同的外部接口

# 说一下base64的编码方式

Base64是一种编码方式。选用大小写字母、数字0-9、+和/的64个可打印字符来表示二进制数据。将二进制数据每三个字节为一组。一共是3 * 8=24bit(位)，划分为四组，每一组为6bit(位)。如果要编码的二进制不是3的倍数，会用00在末尾补足，然后在编码的末尾加上1-2个=号，表示补了多少字节，解码的时候会去掉。将3个字节的二进制数据编码为4字节的文本，解码的时候会去掉。将3字节的二进制数据编码为4字节的文本，是可以让数据在邮件正文、网页等直接显示的。

# 说下 vue-router 中的导航钩子函数

# 说一下React setState原理

# 说说你所理解的中介者模式

# 你所理解的前端路由是什么

# SSL 连接断开后如何恢复

一共有两种方法来恢复断开的 SSL 连接，一种是使用 session ID，一种是 session ticket。

使用 session ID 的方式，每一次的会话都有一个编号，当对话中断后，下一次重新连接时，只要客户端给出这个编号，服务器如果有这个编号的记录，那么双方就可以继续使用以前的秘钥，而不用重新生成一把。

目前所有的浏览器都支持这一种方法。但是这种方法有一个缺点是，session ID 只能够存在一台服务器上，如果我们的请求通过负载平衡被转移到了其他的服务器上，那么就无法恢复对话。

另一种方式是 session ticket 的方式，session ticket 是服务器在上一次对话中发送给客户的，这个 ticket 是加密的，只有服务器能够解密，里面包含了本次会话的信息，比如对话秘钥和加密方法等。

这样不管我们的请求是否转移到其他的服务器上，当服务器将 ticket 解密以后，就能够获取上次对话的信息，就不用重新生成对话秘钥了。

# 说一下ajax/axios/fetch三者的区别

# 微服务有什么好处

# Reflect 对象创建目的是什么

# require模式引入的查找方式是什么

# addEventListener再removeListener会不会造成内存泄露

# CDN 访问过程是什么

1.用户输入访问的域名,操作系统向 LocalDns 查询域名的 ip 地址.

2.LocalDns 向 ROOT DNS 查询域名的授权服务器(这里假设 LocalDns 缓存过期)

3.ROOT DNS 将域名授权 dns 记录回应给 LocalDns

4.LocalDns 得到域名的授权 dns 记录后,继续向域名授权 dns 查询域名的 ip 地址

5.域名授权 dns 查询域名记录后(一般是 CNAME )，回应给 LocalDns

6.LocalDns 得到域名记录后,向智能调度 DNS 查询域名的 ip 地址

7.智能调度 DNS 根据一定的算法和策略(比如静态拓扑，容量等),将最适合的 CDN 节点 ip 地址回应给 LocalDns

8.LocalDns 将得到的域名 ip 地址，回应给 用户端

9.用户得到域名 ip 地址后，访问站点服务器

10.CDN 节点服务器应答请求，将内容返回给客户端.(缓存服务器一方面在本地进行保存，以备以后使用，二方面把获取的数据返回给客户端，完成数据服务过程)

# node性能如何监控

node应用监控主要分两大类：业务逻辑型的监控和硬件方面的监控。

性能监控：

- 日志监控 可以通过监控异常日志的变动，将新增的异常类型和数量反映出来 监控日志可以实现pv和uv的监控，通过pv/uv的监控，可以知道使用者们的使用习惯，预知访问高峰

- 响应时间 响应时间也是一个需要监控的点。一旦系统的某个子系统出现异常或者性能瓶颈将会导致系统的响应时间变长。响应时间可以在nginx一类的反向代理上监控，也可以通过应用自己产生访问日志来监控

- 进程监控 监控日志和响应时间都能较好地监控到系统的状态，但是它们的前提是系统是运行状态的，所以监控进程是比前两者更为紧要的任务。监控进程一般是检查操作系统中运行的应用进程数，比如对于采用多进程架构的web应用，就需要检查工作进程的数，如果低于低估值，就应当发出警报

- 磁盘监控 磁盘监控主要是监控磁盘的用量。由于写日志频繁的缘故，磁盘空间渐渐被用光。一旦磁盘不够用将会引发系统的各种问题，给磁盘的使用量设置一个上限，一旦磁盘用量超过警戒值，服务器的管理者应该整理日志或者清理磁盘

- 内存监控 对于node而言，一旦出现内存泄漏，不是那么容易排查的。监控服务器的内存使用情况。如果内存只升不降，那么铁定存在内存泄漏问题。符合正常的内存使用应该是有升有降，在访问量大的时候上升，在访问量回落的时候，占用量也随之回落。监控内存异常时间也是防止系统出现异常的好方法。如果突然出现内存异常，也能够追踪到近期的哪些代码改动导致的问题

- cpu占用监控 服务器的cpu占用监控也是必不可少的项，cpu的使用分为用户态、内核态、IOWait等。如果用户态cpu使用率较高，说明服务器上的应用需要大量的cpu开销；如果内核态cpu使用率较高，说明服务器需要花费大量时间进行进程调度或者系统调用；IOWait使用率反映的是cpu等待磁盘I/O操作；cpu的使用率中，用户态小于70%，内核态小于35%且整体小于70%，处于正常范围。监控cpu占用情况，可以帮助分析应用程序在实际业务中的状况。合理设置监控阈值能够很好地预警

- cpu load监控 cpu load又称cpu平均负载。它用来描述操作系统当前的繁忙程度，又简单地理解为cpu在单位时间内正在使用和等待使用cpu的平均任务数。它有3个指标，即1分钟的平均负载、5分钟的平均负载，15分钟的平均负载。cpu load过高说明进程数量过多，这在node中可能体现在用于进程模块反复启动新的进程。监控该值可以防止意外发生

- I/O负载 I/O负载指的主要是磁盘I/O。反应的是磁盘上的读写情况，对于node编写的应用，主要是面向网络业务，是不太可能出现I/O负载过高的情况，大多数的I/O压力来自于数据库。不管node进程是否与数据库或其他I/O密集的应用共同处理相同的服务器，我们都应该监控该值防止意外情况

- 网络监控 虽然网络流量监控的优先级没有上述项目那么高，但还是需要对流量进行监控并设置流量上限值。即便应用突然受到用户的青睐，流量暴涨的时候也可以通过数值感知到网站的宣传是否有效。一旦流量超过警戒值，开发者就应当找出流量增长的原因。对于正常增长，应当评估是否该增加硬件设备来为更多用户提供服务。网络流量监控的两个主要指标是流入流量和流出流量

- 应用状态监控 除了这些硬性需要检测的指标之外，应用还应该提供一种机制来反馈其自身的状态信息，外部监控将会持续性地调用应用地反馈接口来检查它地健康状态

- dns监控 dns是网络应用的基础，在实际的对外服务产品中，多数都对域名有依赖。dns故障导致产品出现大面积影响的事件并不少见。由于dns服务通常是稳定的，容易让人忽略，但是一旦出现故障，就可能是史无前例的故障。对于产品的稳定性，域名dns状态也需要加入监控

# 为什么useState要使用数组而不是对象

useState运用了JS的解构思想。对象和数组的解构赋值区别是：

- 数组元素是有顺序的，数组解构时变量的取值由数组元素的位置决定，变量名可以任意命名

- 对象的属性是没有顺序的，解构时变量必需与属性同名才能取到正确的值

由此可以看出，数组会更加灵活，可以任意命名state和修改state的方法名。而useState内部原理是把state声明成一个数组，需要顺序一一对应。由于一个组件可以使用多个useState，为了避免冲突并确保state的准确性，useState要使用数组而不是对象。

# Node 更适合处理 I/O 密集型任务还是 CPU 密集型任务,为什么？

Node 更适合处理 I/O 密集型的任务。因为 Node 的 I/O 密集型任务可以异步调用，利用事件循环的处理能力，资源占用极少，并且事件循环能力避开了多线程的调用，在调用方面是单线程，内部处理其实是多线程的。

由于 Javascript 是单线程的原因，Node 不适合处理 CPU 密集型的任务，CPU 密集型的任务会导致 CPU 时间片不能释放，使得后续 I/O 无法发起，从而造成阻塞。但是可以利用到多进程的特点完成对一些 CPU 密集型任务的处理，不过由于 Javascript 并不支持多线程，所以在这方面的处理能力会弱于其他多线程语言（例如 Java、Go）。

# 什么是微服务

所谓的微服务是SOA架构下的最终产物，该架构的设计目标是为了肢解业务，使得服务能够独立运行

微服务可以按照业务划分，将一组特定的业务划分成一个服务，每个服务都有自己对的数据库，独立部署，服务直接通过Rest API进行通讯。每一个独立运行的服务组成整合系统

总结下，微服务是，由单一应用程序构成的小服务，拥有自己的进程与轻量化处理，服务依业务功能设计，以全自动的方式部署，与其他服务使用HTTP api通讯。同时，服务会使用最小的规模的集中管理(例如docker)技术，服务可以用不同的编程语言与数据库等。微服务架构是将复杂臃肿的单体应用进行细粒度的服务化拆分，每个拆分出来的服务各自独立打包部署，并交由小团队进行开发和运维，从而极大地提高了应用交付地效率

微服务设计的原则： 各司其职 服务高于可用性和可扩展性

# vue双向数据绑定原理

# 说一下你理解的CORS

# 什么是 CDN 服务

CDN 是一个内容分发网络，通过对源网站资源的缓存，利用本身多台位于不同地域、不同运营商的服务器，向用户提供资源就近访问的功能。也就是说，用户的请求并不是直接发送给源网站，而是发送给 CDN 服务器，由 CDN 服务器将请求定位到最近的含有该资源的服务器上去请求。这样有利于提高网站的访问速度，同时通过这种方式也减轻了源服务器的访问压力。

# 实现单点登录的原理

# 介绍下你所理解的React设计思路,它的理念是什么

# node性能如何优化

# 微服务和单体应用的区别

# 神奇的null

```
// 请输出结果并进行解释
console.log([typeof null, null instanceof Object])
```

答案为：["object", false]

在MDN关于 null 的文档中也特别指出来了，typeof null 的结果是 "object"，它是ECMAScript的bug，其实应该是 "null"。但这个bug由来已久，在JavaScript中已经存在了将近二十年，也许永远不会修复，因为这牵扯到太多的Web系统，修复它会产生更多的bug，令许多系统无法正常工作。而 instanceof 运算符是用来测试一个对象在其原型链构造函数上是否具有 prototype 属性，null 值并不是以 Object 原型建出来的，所以 null instanceof Object 返回 false。

# 优先级顺序  
```
请输出结果并进行解释
var val = 'smtg';
console.log('Value is ' + (val === 'smtg') ? 'Something' : 'Nothing');
```

答案是："Something"，因为 + 的优先级比条件运算符 condition ? val1 : val2 的优先级高。

# jsonp的工作原理

jsonp是一种跨域通信的手段，原理是通过script标签的src属性来实现跨域。实现机制如下：

1. 与服务端约定好一个回调函数名称，在客户端定义好这个函数，在请求url中添加callback=函数名的查询字符

2. 服务端接收到请求之后，将函数名和需要返回的数据，拼接成函数名(data)函数执行的形式返回

3. 页面接收到数据后，解析完成直接执行这个回调函数，这个时候数据就成功传输了客户端

# Redux 中间件是如何拿到store和action

redux中间件本质就是一个柯里化函数。

- redux applyMiddleware api源码，每个applyMiddleware接收2个参数，store的getState函数和dispatch函数，分别获得store和action，最终返回一个函数

- 该函数会被传入next的下一个middleware的dispatch方法，并返回一个接收action的新函数，这个函数可以直接调用next(action)，或者在其他需要的时刻去调用，或者不去调用

- 调用链中最后一个middleware会接收store的dispatch方法作为next参数，并且借此结束调用链

所以，middleware的函数时({getState,dispatch}) => next => action

# 介绍你所理解的组合模式

定义：组合模式（Composite Pattern），又叫“部分-整体”模式，是用于把一组相似的对象当作一个单一的对象。组合模式依据树形结构来组合对象，用来表示部分以及整体层次。这种类型的设计模式属于结构型模式，它创建了对象组的树形结构。

这种模式创建了一个包含自己对象组的类。该类提供了修改相同对象组的方式。

优点：
- 高层模块调用简单
- 节点自由增加

缺点：
- 在使用组合模式时，其叶子和树枝的声明都是实现类，而不是接口，违反了依赖倒置原则。

# 了解函数式编程中的compose么

将多个函数的能力合并，创造一个新的函数。compose函数可以接受任意的参数，所有的参数都是函数，且执行方向是自右向左的，初始函数一定放到参数的最右面。

```
const compose=(...fns)=>(...args)=>{
  const [...tmpFns]=fns;
  const composed=(...restArgs)=>{
    if(tmpFns.length===0){
      return restArgs[0];
    }
    return composed(tmpFns.pop()(...restArgs));
  };
  return composed(...args);
};
```

# 对称加密和非对称加密的区别和用处

对称加密：对称加密采用了对称密码编码的技术，它的特点是文件加密和解密使用相同的密钥加密，也就是密钥也可以用作解密密钥，这种方法在密码学中叫做对称加密算法，对称加密算法使用起来简单快捷，密钥较短且破译困难，除了数据加密标准(DES),另一个对称密钥加密系统是国际数据加密算法(IDEA),它比DES的加密性好，而且对计算机功能要求也没有那么高。

- 对称加密：收发双方规定密钥
- 加密的人也能解密，这就是对称

问题：密钥需要传递，传递的过程中，可能被窃听和纂改

非对称加密: 与对称加密算法不同，非对称加密算法需要两个密钥：公开密钥和私有密钥。公开密钥和私有密钥是一对，如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密；如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密。因为加密和解密使用的是两个不同的密钥，所以这种算法叫做非对称加密算法

非对称加密算法实现机密信息交换的基本过程是:甲方生成一对密钥并将其中的一把作为公用密钥向其它方公开;得到该公用密钥的乙方使用该密钥对机密信息进行加密后在发送给甲方;甲方再用自己保存的另一把专用密钥对加密后的信息进行解密。甲方只能用其专用密钥解密由其公用密钥加密后的任何信息

非对称加密的典型应用是数字签名。常见的非对称加密算法有：RSA,ECC(移动设备使用),Diffie-Hellman,EIGamal,DSA(数字签名使用)

- 发送人留着钥匙，把带锁的盒子传过去，加密的人锁上，但是解不开，就是非对称

问题：可能被窃听更换掉盒子（认证机构来给盒子做签名，也就是我们HTTPS需要的网站证书）

区别：

- 对称加密只需要一把密钥，非对称加密需要一对密钥(公钥和密钥)

- 对称加密 算法简单，加密解密容易，效率高，执行快；只有一把钥匙，密文如果被拦截，且密钥也被劫持，那么，信息很容易被破译，安全性能低；非对称加密算法及其复杂，安全性依赖算法与密钥，而且加密和解密效率很低；即使密文被拦截、公钥被获取，但是无法获取到私钥，也就无法破译密文，安全性能高

所以，非对称可靠但是慢，对称高效但不可靠，若配合使用，非对称加密进行身份验证和密钥交换，对称加密进行数据的加密，可达到最好的效果。

# Vue是如何收集依赖的

# 介绍你所理解的迭代器模式

# JS为什么要区分微任务和宏任务

# 讲一下你所了解的函数式编程

# 介绍你所理解的单例模式

定义：

单例模式（Singleton Pattern）是 Java 中最简单的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

主要解决：一个全局使用的类频繁地创建与销毁。

优点：
- 在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例（比如管理学院首页页面缓存）。
- 避免对资源的多重占用（比如写文件操作）。
- 
缺点：
- 没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化

# Vue-cli默认是单页面的，如果要开发多页面应该怎么办

# js异步解决方案有哪几种
回调函数（callback）

- 优点：逻辑简单
- 缺点：深层级产生回调地狱

Promise

- 优点：一旦状态改变就不会在变，任何时候都可以得到这个结果;可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数
- 缺点：无法取消，当处于pengding状态时，无法得知目前进展到哪一个阶段

Generator

- 优点：执行可控；每一步可以传递数据，也可以传递异常
- 缺点：控制流程比较复杂，成本比较高

async/await

- 优点：代码清晰，不许需要链式调用就可以处理回调地狱的问题；错误的话可以被try catch
- 缺点：控制流程复杂，成本较高

此外，还可以通过事件监听、发布/订阅等方式解决异步问题。

# 介绍class和ES5的类以及区别
ES5的类：function

class：类声明创建一个基于原型继承的具有给定名称的新类

区别：
- 类声明不可以提升
- 类声明不允许再次声明已经存在的类，否则将会抛出一个类型错误
- class内部是严格模式，构造函数是可选的
- class的静态方法或者原型方法都不可枚举，并且这些方法都没有原型，不可被new
- class必须使用new 来调用
- class内部无法重写类名

# 说说Vue开发如何针对搜索引擎做SEO优化

虽然SPA单页面应用对SEO不友好，但是也有相应的解决方案。如果构建大型网站，比如商城类，直接上SSR服务器渲染；如果是个人博客、公司官网这类，其余三种都可以；如果对已用SPA开发完成的项目进行SEO优化，而且支持node服务器，请使用Phantomjs。

- SSR服务器渲染
Vue.js是构建客户端应用程序的框架。默认的情况下，可以在浏览器中输出Vue组件，进行生成DOM和操作DOM。然而，也可以将同一个组件渲染为服务器端的html字符串，将它们直接发送到浏览器，最后将这些静态标记为"激活"为客户端上完全可交互的应用程序。服务器渲染的 Vue.js 应用程序也可以被认为是"同构"或"通用"，因为应用程序的大部分代码都可以在服务器和客户端上运行。
```
权衡的地方：

    开发条件所限，浏览器特定的代码，只能在某些生命周期钩子函数中使用；一些外部扩展库可能需要特殊处理，才能在服务器渲染应用程序中运行
    
    环境和部署要求更高，需要node.js server 运行环境
    
    高流量的情况下，需要准备相应的服务器负载，并明智地采取缓存策略
    

优势:

    更好的seo，因为搜索引擎爬虫抓取工具可以直接查看完全渲染的页面
    
    更快的内容到达时间，特别是对于缓慢的网络情况或运行缓慢的设备
    

不足：

    一套代码两套执行环境，会引发各种问题，比如服务端没有window、document对象，处理方式是增加判断，如果是客户端才可以执行
    
    涉及构建设置和部署的更多要求，需要处于node server的运行环境
    
    更多的服务端负载
```

- Nuxt 静态化
Nuxt是一个基于Vue生态的更高层的框架，为开发服务端渲染的Vue应用提供了极其便利的开发体验。更酷的是：可以用它来作为静态站生成器。
静态化是Nuxt.js打包的另一种方式，算是Nuxt.js的一个创新点，页面加载速度很快，需要注意的是:在Nuxt.js执行generate静态化打包时，动态路由会被忽略。
```
优势:

    纯静态文件，访问速度超快
    
    对比SSR，不涉及到服务器负载方面问题
    
    静态网页不宜遭到黑客攻击，安全性更高
    
不足：

    如果动态路由参数多的话不适用
```

- 预渲染 prerender-spa-plugin
如果你只是用来改善少数营销页面(例如/，/about/，/contact等)的seo，那么你可能需要预渲染。无需使用web服务器实时动态编译html，而是使用预渲染的方式，在构建时简单地生成针对特定路由地静态HTML文件。优点就是设置预渲染更简单，并可以将你的前端作为一个完全静态的站点。
```
优势：

    改动小，引入插件配置即可
    
不足： 

    无法使用动态路由
    
    只适用少量页面的项目，页面多达几百个的情况下打包会非常慢
```

- 使用Phantomjs针对爬虫做处理
Phantomjs 是基于一个 webkit内核的无头浏览器，即没有UI界面，即它就是一个浏览器，只是其内的点击、翻页等为人相关操作需要程序设计实现。虽然"Phantomjs 宣布终止开发"，但是已经满足对Vue的SEO处理。
这种解决方案其实是一种旁路机制，原理就是通过 nginx 配置，判断访问的来源 UA 是否爬虫访问，如果是则就将搜索引擎的爬虫请求转发到一个 node server，在通过Phantomjs 来解析完整的html，返回给爬虫。 
```
优势：

    完全不用改动项目代码，按照原本的spa开发即可，对比开发SSR成本小不要太多
    
    对已用SPA开发完成的项目，这是最好的选择
    
不足：

    部署需要node服务器支持
    
    爬虫访问比网页访问要慢一些，因为定时要定时资源加载完成才返回给爬虫
    
    如果被恶意模拟百度爬虫大量循环爬取，会造成服务器负载方面问题，解决方法是判断访问的ip，是否是百度官方爬虫的ip
```

# 介绍你所理解的工厂模式

# Promise.reslove(obj),obj有几种形式

# 说说ES6对Object类型做了哪些优化更新

# 介绍你所理解的装饰器模式

# 虚拟列表是什么？说一下它的实现原理

# 说一下 JavaScript 的宿主对象和原生对象的区别

# 浏览器都有哪些进程，渲染进程中都有什么线程

# 什么是跨域?都有哪些方式会造成跨域，常见的解决跨域的方式有哪些

跨域指的是非同源的资源之间尝试着进行交互通信，而由于受浏览器同源策略的限制，无法正常进行交互通信。 浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏览器对JS实施的安全限制。无法跨域是浏览器对于用户安全的考虑，同源策略限制了以下行为：Cookie、LocalStorage和IndexDB 无法读取DOM和JS对象无法获取，ajax请求发送不出去。

非同源请求、服务端设置cors限制会造成跨域。

常见解决跨域的方式

- 利用jsonp进行跨域。是最常见的跨域方式之一。

- window.name+iframe window.name通过在iframe（一般动态创建）中加载跨域HTML文件来起作用。然后，HTML文件将传递给请求者的字符串内容赋值给window.name。然后，请求者可以检索window.name值作为响应。

- window.postMessage() HTML5新特性，可以用来向其他所有的 window 对象发送消息。需要注意的是我们必须要保证所有的脚本执行完才发送 MessageEvent，如果在函数执行的过程中调用了它，就会让后面的函数超时无法执行。

- WebSocket WebSocket protocol 是HTML5一种新的协议。它实现了浏览器与服务器全双工通信，同时允许跨域通讯，是server push技术的一种很棒的实现。

- 图片ping或script标签跨域 图片ping常用于跟踪用户点击页面或动态广告曝光次数。script标签可以得到从其他来源数据，这也是JSONP依赖的根据。缺点：只能发送Get请求 ，无法访问服务器的响应文本（单向请求）


# 请问如何进行首页加载优化

- CDN分发: 通过在多台服务器部署相同的副本，当用户访问时，服务器根据用户跟哪台服务器地理距离小或者哪台服务器此时的压力小，来决定哪台服务器去响应这个请求

- 后端在业务层的缓存:数据库查询缓存是可以设置缓存的，这个对处于高频率的请求是很有用。值得注意的是，接口也是可以设置缓存的，比如获取一定时间内不会变的资源，设置缓存会很有用

- 静态文件缓存方案: 现在流行的方式是文件hash+强缓存的一个方案。比如hash+cache control:max-age=1年

- 前端的资源动态加载:

1. 路由动态加载，是最常用的方法，以页面为单位，进行动态加载
 
2. 组件动态加载，对于不在当前视窗的组件，先不加载
 
3. 图片懒加载，越来越多的浏览器支持原生的懒加载，通过给img标签加上 loading="lazy"来开启懒加载模式

利用好async和defer这两个属性: 如果是独立功能的js文件，可以加入async属性。如果是优先级低并且没有依赖的js，我们可以加入defer属性。

- 渲染的优先级: 浏览器有一套资源的加载优先级策略。也可以通过js来自己控制请求的顺序和渲染的顺序。一般我们不需要这么细粒度的控制，而且控制的代码也不好写。

- 前端做一些接口缓存:前端也可以做接口缓存，缓存的位置有两个，一个是内存，即保存给变量，另一个是localStorage。比如用户的签到日历(展示用户是否签到)，我们可以缓存这样的接口到localStorage，有效期是当天。或者有个列表页面，我们总是缓存上次的列表内容到本地，下次加载时，我们先从本地读取缓存，并同时发起请求到服务器获取最新列表

- 页面使用骨架屏: 在首屏加载完成之前，通过渲染一些简单元素进行占位。骨架屏虽然不能提高首屏加载速度，但可以减少用户在首屏等待的急躁心情

- 引入http2.0： http2对比http1.1，最主要的提升是运输性能，特别在接口小而多的时候

- 利用好http压缩:使用http压缩的效果会非常明显

# 介绍下浏览器事件流向

DOM2级事件规定的事件流包括三个阶段：事件捕获阶段，处于目标阶段，事件冒泡阶段。

事件捕获阶段（Event Capturing）： 事件捕获的用意是在于事件到达预定目标之前捕获它。因此，事件捕获的过程是让不太具体的节点先更早接收到事件，而最具体的节点应该最后接收到事件。

冒泡阶段（Event Bubbling）： 事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点，即document对象。

DOM2 与 DOM0区别：

DOM2级事件定义了两个方法，用于处理指定和删除事件处理程序的操作：addEventListener，removeEventListener

# 说一下 Vue3 的 Composition API

# cdn分布式部署，如何处理用户请求最近的资源

# 说一下 let、const 的实现，使用 ES5 模拟实现

# 介绍冒泡排序、选择排序，说说冒泡排序如何优化

# 前端怎样做单元检测

# 301、302、304 的区别

# 什么是同源策略

# Vue-router history 模式部署的时候要注意什么?server 端用 nginx 和 node 时候分别怎么处理?

# 说一下递归和迭代的区别是什么，各有什么优缺点?

# 说一下对vue3.0的了解，vue3.0为什么要用代理?

# 手写一个观察者模式
