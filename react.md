# React 相关面试题

# React Hooks 当中的 useEffect 是如何区分生命周期钩子的？

useEffect 可以看成是 componentDidMount、componentDidUpdate 和 componentWillUnmount 三者的结合

useEffect(callback，[dependencies])接受两个参数，调用方式如下：
```
useEffect(() => {
  consoloe.log("mounted");
  return () => {
    console.log("willUnmount");
  };
}, [dependencies]);
```
生命周期函数的调用主要是通过第二个参数[dependencies]来进行控制，有如下几种情况：

- [dependencies]参数不传时，则每次都会优先调用上次保存的函数中返回的那个函数，然后在调用外部那个函数

- [dependencies]参数传[]时，则外部的函数只会在初始化时调用一次，返回的那个函数也只会最终在组件卸载时调用一次

- [dependencies]参数有值时，则只会监听到数组中的值发生变化后才优先调用返回的那个函数，在调用外部的函数

# Redux 中的 connect 有什么作用?

connect 负责连接 React 和 Redux。

- 获取 state

connect 通过 context 获取 Provider 中的 store，通过 store.getState()获取整合 store tree 上所有 state

- 包装原组件

将 state 和 action 通过 props 的方式传入到原组件内部 WrapWithConnent 返回一个 ReactComponent 对象 Connent，Connect 重新 redner 外部传入的原组件 WrappedComponent，并把 connect 中传入的 mapStateToProps，mapDispatchToProps 与组件上原有的 props 合并后，通过属性的方式传递给 WrappedComponent

- 监听 store tree 变化

connect 缓存 store tree 中 state 的状态，通过当前 state 状态和变更前 state 状态进行比较，从而确定是否调用 this.setState()方法触发 Connect 及其子组件的重新渲染

# React 构建组件的方式有哪些?有什么区别?

React组件的创建主要分成了三种方式：

1.函数式创建

2.通过 React.createClass 方法创建

3.继承 React.Component 创建

### 区别

由于 React.createClass 创建的方式过于冗杂，并不建议使用。而像函数式创建和类组件创建的区别主要在于需要创建的组件是否需要为有状态的组件：

对于一些无状态的组件创建，建议使用函数式创建的方式

由于react hooks的出现，函数式组件创建的组件通过hooks方法也能使之成为有状态组件，在加上目前推崇函数式编程，所以这里建议都使用函数式的方式来创建组件

在考虑组件的选择原则上，能用无状态组件则用无状态组件

# React Fiber 是如何实现更新过程可控?

Fiber 是比线程（Thread）控制得更精密的执行模型。简单点说，Fiber 就是 React 16 实现的一套新的更新机制，让 React 的更新过程变得可控，避免了之前一竿子递归到底影响性能的做法。

更新过程的可控主要体现在下面几个方面：

- 任务拆分：将调和阶段（Reconciler）递归遍历 VDOM 这个大任务分成若干小任务，每个任务只负责一个节点的处理

- 任务挂起、恢复、终止：workInProgress 代表当前正在执行更新的 Fiber 树，这棵树在构建每一个节点的时候会收集当前节点的副作用，整棵树构建完成后，会形成一条完整的副作用链；currentFiber 表示上次渲染构建的 Filber 树，在每一次更新完成后 workInProgress 会赋值给  currentFiber。在新一轮更新时 workInProgress tree 再重新构建，新 workInProgress 的节点通过 alternate 属性和 currentFiber 的节点建立联系。在新 workInProgress tree 的创建过程中，会同 currentFiber 的对应节点进行 Diff 比较，收集副作用。同时也会复用和 currentFiber 对应的节点对象，减少新创建对象带来的开销，任务挂起、恢复、终止 整个过程发生在 workInProgress tree 创建过程中

![任务调度](https://static001.geekbang.org/infoq/82/82943272cfb62fefcee943cb845d26e4.webp)

- 任务具备优先级：具体点就是在创建或者更新 FiberNode 的时候，通过算法给每个任务分配一个到期时间（expirationTime）。在每个任务执行的时候除了判断剩余时间，如果当前处理节点已经过期，那么无论现在是否有空闲时间都必须执行改任务

# React 中的 ref 有什么用?

使用 refs 获取组件被调用时会新建一个该组件的实例。refs 会指向这个实例，可以是一个回调函数，回调函数会在组件被挂载后立即执行。

如果把 refs 放到原生 DOM 组件的 input 中，我们就可以通过 refs 得到 DOM 节点；如果把 refs 放到 React 组件中，那么我们获得的就是组件的实例，因此就可以调用实例的方法(如果想访问该组件的真实 DOM，那么可以用 React.findDOMNode 来找到 DOM 节点

## 说说 React 状态逻辑复用问题

## 你知道的React性能优化有哪些方法？
1、react性能查看工具

查看react加载组件时所耗费的时间的工具，在react 16版本之前我们可以使用React Perf来查看。也可以在chorme中先安装React Perf扩展，然后在入口文件或者redux的store.js中加入相应的代码即可。

2、渲染角度优化

（1）使用immutable.js

（2）不要在render中修改状态

（3）不在元素中使用内联样式，使用css隐藏节点而不是强制加载和卸载

（4）使用SSR，可以在服务端生成html后返回到客户端，使客服端能快速看到完整渲染的页面

（5）使用React.Fragment减少不必要DOM

3、组件层面优化

（1）组件懒加载。组件或UI库也可以使用动态导入的方式，只在用户使用到的时候加载。页面组件可以使用react-loadable。

（2）使用pureComponent代替component，以达到一些没必要的渲染，或者在使用shouldComponent进行一个优化。

（3）组件尽可能的拆分解耦，给列表类组件提供唯一不变的key，尽量不要使用下标作为key。

（4）在constructor中使用bind来绑定this，而不在使用时绑定或减少使用箭头函数，因为constructor只在组件初始化时执行一次，而使用时绑定是每次render都会执行，箭头函数也是如此。

（5）按需引入props，避免多余更新。

4、数据获取层面优化

（1）不要在componentWillMount中请求数据

（2）redux与reselect结合使用，reselect动作的原理是只要相关的状态没有改变，那么就直接使用上一次的缓存结果。

（3）结合业务场景使用localstorage、sessionstorage等缓存机制。

5、代码打包编译层面优化

（1）结合打包工具webpack、gulp等使用，一般常用webpack，利用webpack打包分离去重实现动态导入，减少重复性代码块。

（2）webpack结合plugin+loader使用。

## 你对immutable有了解吗？它有什么作用？
1、Immutable实现的原理

Immutable实现的原理是利用结构共享形成持久化数据结构，也就是使用旧数据创建新数据时，要保证旧数据同时可用且不变。同时为了避免 deepCopy 把所有节点都复制一遍带来的性能损耗，Immutable使用了结构共享，即如果对象树中一个节点发生变化，只修改这个节点和受它影响的父节点，其它节点则进行共享。

2、Immutable的优点

（1）节约内存

JavaScript 中的对象一般是可变的（Mutable），因为使用了引用赋值，新的对象简单的引用了原始对象，改变新的对象将影响到原始对象。为了解决这个问题，一般的做法是使用shallowCopy（浅拷贝）或 deepCopy（深拷贝）来避免被修改，但这样做造成了CPU和内存的浪费。Immutable 可以很好地解决这些问题。

（2）Undo/Redo，Copy/Paste，时间轴等功能容易实现

因为每次数据都是不一样的，只要把这些数据放到一个数组里储存起来，想回退到哪里就拿出对应数据即可，很容易开发出撤销重做这种功能。

（3）并发安全

Immutable Data一旦创建，就不能再被更改,也就不需要并发锁。

3、Immutable使用

（1）与React搭配使用，Immutable简洁高效的判断数据是否变化，提高渲染速度及性能

（2）与Redux/flux搭配使用

## 在React中创建动画有哪些方式
创建React动画有以下几种：

1.基于定时器或requestAnimationFrame的间隔动画；使用定时器可能会有掉帧问题，而使用requestAnimationFrame则性能较好，完全使用js，不依赖css，帧数跟屏幕刷新率一致，页面运行到后台会自动暂停提高性能。

2.基于css3中的animation和transition简单动画；有较高的性能，代码量少，但是只能依赖于css效果，对于复杂动画比较难实现跟控制。

3.React动画插件CssTransitionGroup；性能比较好，但限定于入场跟出场场景。

4.其他第三方动画库。

## React为什么要搞Hooks，React Hooks帮我们解决了哪些问题
React Hooks是React 16.8的新增特性。它可以让你在不编写class的情况下使用state及其他React的特性（如：可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React）。
Hooks是一种更简单的方式，用于封装用户界面中的有状态行为和副作用。

Hook 使用规则：
* 只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用。
* 只能在 React 的函数组件中调用 Hook。不要在其他 JavaScript 函数中调用。（还有一个地方可以调用 Hook —— 就是自定义的 Hook 中）

React Hooks 出现之前，UI 组件我们可以使用函数，无状态组件来展示 UI，而对于容器组件，函数组件就显得无能为力，我们依赖于类组件来获取数据，处理数据，并向下传递参数给 UI 组件进行渲染,无状态函数，是通过函数来创建组件，这样的好处是它在创建时，只会保持一个实例，避免了不必要的内存分配和检查，我们应该使用无状态组件。但是它的问题在于它不存在state和生命周期。而Hook 的出现，解决了这个问题。

React Hooks相比于类组件有以下的好处:

* 代码可读性更强，原本同一块功能的代码逻辑被拆分在了不同的生命周期函数中，容易使开发者不利于维护和迭代，通过 React Hooks 可以将功能代码聚合，方便阅读维护
* 组件树层级变浅，在原本的代码中，我们经常使用 HOC/render props 等方式来复用组件的状态，增强功能等，无疑增加了组件树层数及渲染，而在 React Hooks 中，这些功能都可以通过强大的自定义的 Hooks 来实现

## 怎么实现React组件的国际化
国际化的主要原理：
通过改变语言状态来切换不同的语言配置文件（该文件可以是json或js文件），解析配置文件进行渲染。

一般多语言国际化这种全局需求，我们可以使用React的context来全局共享数据，包含："当前语言"和一些通用词汇语言包。

React组件本身也可以维护一套自己的语言包，例如时间选择器等，通过获取全局的"当前语言"，然后通过映射获取指定位置的字符，进行拼接或展示。

在应用过程中，注意以下几点:
* 切换语言是一个低频需求，但语言包可能会比较大，可以按需加载
* 限制词语或句子的长度，在语言切换时，长度可能发生变化。比如，英文单词可能比中文长，会影响布局
* 注意颜色在不同语言、文化中的差异
* 注意日期和货币格式在不同国家和地区的差异

## 什么是受控组件和非受控组件
受控组件和非受控组件是针对表单而言的。受控和非受控之间可互相转化。
* 受控组件
 1. 组件中表单的值（value、checked）受state的控制，需要显式设置value或checked属性。
 2. 需要给表单元素绑定onChange事件，value的值由setState来修改。
 
 使用场景：
 需要对组件的value值进行修改时，使用受控组件。
 
 如：表单的实时校验，添加相应的状态和提示
 
 * 非受控组件
 1. 在表现形式上，表单组件不设置value属性（单选、复选为checked属性）。
 2. 表单的数据由DOM处理，可通过ref获取DOM节点后再获取value的值。
 
 使用场景：
 任何时候都不需要修改value。

## 了解 redux 么，说一下 redux 吧
Redux 本身是个状态管理库,核心或者说目的一句话就能概括, 清晰的描述应用的状态。

Redux 核心和原则

这个应用的状态是一个唯一的状态树
状态是只读的, 只能通过 action 来触发修改, 其实实际修改状态的是 reducer
修改状态只能通过纯函数
Redux 中的概念

1.reducer

reducer 就是实际改变 state 的函数, 在 redux 中, 也只有 reducer 能够改变 state. 根据 redux 的原则, 整个应用只有一个唯一的状态树, 这样, 理论上只要一个 reducer 就够了. 但是, 实际编码时, 如果应用稍具规模, 只有一个 reducer 文件, 显然不利于分模块合作开发, 也不利于代码维护. 所以, reduer 一般是按模块, 或者根据你所使用的框架来组织, 会分散在多个文件夹中. 这时, 可以通过 redux 提供的 API combineReducers 来合并多个 reducer, 形成一个唯一的状态树. reducer 的使用只要注意 2 点:

1、必须是纯函数2、多个 reducer 文件时, 确保每个 reducer 处理不同的 action, 否则可能会出现后面的 reducer 被覆盖的情况

2.state

state 或者说是 store, 其实就是整个应用的状态.

3.action

redux 中的 action 其实就是一个 包含 type 字段的plain object. type 字段决定了要执行哪个 reducer, 其他字段作为 reducer 的参数.

4.action creator

action creator 本质是一个函数, 返回值是一个满足 action 的定义的 plain object. 使用 action creator 的目的就是简化 action 的定义

5.dispath

view层通过action来改变store从而改变当前的state，但是action只是一个对象而已,store.dispatch() 就是 view 发出 Action对象的唯一方法。 dispatch的中文意思就是派遣、发送的意思。 即将action发送到store.

6.subscribe

store允许使用 store.subscripbe 方法设置监听函数，一旦 state 发生变化， 就自动执行这个函数。

7.middleware

redux 的 middleware 发生在 dispatching an action 和 reaches the reducer 之间. 在这个时间点, 除了可以实现异步操作, 还可以实现 logging等等.

## 描述事件在React中的处理方式
React 元素的事件处理和 DOM 元素的很相似，但是有一点语法上的不同：

React 事件的命名采用小驼峰式（camelCase），而不是纯小写。
使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串。 在 React 中另一个不同点是你不能通过返回 false 的方式阻止默认行为。你必须显式的使用 preventDefault 。
在React中的event是一个合成事件，React 根据 W3C 规范来定义这些合成事件，所以你不需要担心跨浏览器的兼容性问题。另外，在合成事件中只能阻止合成事件中的事件传播。合成事件中的stopPropagation无法阻止事件在真正元素上的传递，它只阻止合成事件中的事件流。

在合成事件系统中，所有的事件都是绑定在document元素上，即，虽然我们在某个react元素上绑定了事件，但是，最后事件都委托给document统一触发。

## context 是什么，有什么作用
React Context提供了一种方式，能够让数据在组件树中传递，而不必一级一级手动传递。

如果使用props或者state进行多级数据传递，则数据需要自顶下流经过每一级组件，无法跨级。而context是基于树形结构共享数据的方式，在某个节点组件开启提供context后，所有后代节点组件都可以获取到共享的数据。

context的使用模式是生产消费模式，即生产组件提供数据，消费组件获取数据。

可以通过Provider组件的value来传递数据，也可以通过调用react.createContext()来产生context，然后在Consumer组件获得context中的数据。一个生产组件可以和多个消费组件有对应关系。多个Provider组件也可以嵌套使用，里层的会覆盖外层的数据。

## react 中 props 和 state 是什么，有什么区别
在React中props和state都属于组件的数据，他们的改变都可能会触发组件的重新渲染。

其中props 是组件对外的接口，对于传入的组件而言时可读的、不可变的，遵循单向数据流原则；state 是维护组件内部状态的， 是可变的。

组件内可以引用其他组件，组件之间的引用形成了一个树状结构，如果下层组件需要使用上层组件的数据或方法，上层组件就可以通过下层组件的props属性进行传递，因此props是组件对外的接口，用于组件间的通信。props不能通过子组件自身的方法修改，只能通过父组件传递的回调函数在父组件进行修改。
组件除了使用上层组件传递的数据外，自身也可能需要维护管理数据，这就是组件对内的接口state。修改组件内部状态需要使用setState或forceUpdate方法来改变。
根据对外接口props 和对内接口state，组件计算出对应界面的UI。
主要区别：

state是可变的，是一组用于反映组件UI变化的状态集合；
props对于使用它的组件来说，是只读的，要想修改props，只能通过该组件的父组件修改。
在组件状态提升的场景中，父组件正是通过子组件的props, 传递给子组件其所需要的状态。
没有state的组件叫做无状态组件，它接收props，只负责渲染，反之则叫做有状态组件。工作中应尽量使用无状态组件，增加代码的可维护性和复用性。
## refs 的作用
refs 用于获取到组件实例或者真实的DOM节点 常用于非受控组件

不能在函数式组件上直接使用refs,函数式组件没有实例。但可以在函数式组件内部使用 ref，只要它指向一个 DOM 元素或者 class 组件。
使用方式：

直接指定ref = '' ref 是一个字符串，（不推荐）

通过React.createRef()创建，创建的ref 有个 current属性，函数组件如果需要使用，需要使用React.forwardRef 转发一下ref。hoc组件传递ref也存在同样的问题，需要使用React.forwardRef 转发

通过函数 ref={input => this.userName = input} ,获取值需要使用 this.userName.value

## 展示组件和容器组件分别是什么及其应用
展示组件又叫傻瓜组件，它负责UI展示，接收props，不感知数据是如何来的和变动的，传什么他就渲染什么。一般我们声明为无状态函数，但这不是绝对的，他也可以拥有自己的状态，但这些状态应该是与ui表现有关的。它通常包含一些DOM标记和样式。
容器组件负责与store通信，获取，计算数据，更新状态。它描述组件是如何运行的，而不必关注展现。它实际上就是一个高阶组件，一般在react中，它使用connect方法包裹展示组件，内部与store通信，获取数据，监听数据变化，更新数据。
好处是，解耦了界面与业务逻辑，提高了组件的复用性。比如展示组件由于不关心数据来源，那么可以被不同容器组件复用。同时，UI与业务逻辑分开，也方便维护，比如需要改样式，那么直接修改展示组件，数据变动，直接修改容器组件，互不影响。
## 什么是HOC，在工作中如何应用
HOC也就是高阶组件，来源于高阶函数的概念，借助AOP切片编程的思想及装饰器模式，它接收一个组件作为输入并返回一个新的组件。主要是用于逻辑复用，它不改变原有组件，但对其能力进行增强。提高了组件的抽象性、可维护性 但是注意，不能直接通过 Refs 访问到组件实例，因为ref对于组件来说是个特殊的属性，是由react单独处理的，因此需要使用React.forwardRef进行转发才行。

HOC的实现分两种：

属性代理 HOC 对传给 WrappedComponent 的 porps 进行操作。
反向继承 HOC 扩展了 WrappedComponent。由于被动继承，它可以访问 WrappedComponent 的 state(状态)，props(属性)，组件生命周期方法和 render 方法。因此可以做渲染劫持。
应用：比如react-redux中的connect就是一个HOC，它将store上的state和dispatch映射到组件的props中；再比如react-router-dom中的withRouter，它将路由属性传递到被包裹的非路由组件上，从而使得非路由组件也能访问和操作路由。再有就是日志记录型组件，在组件运行前、中、后对组件的一些状态的获取记录等。
