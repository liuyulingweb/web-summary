# 深入 React 技术栈
> React 之所以流行，在于它平衡了函数式编程（把 DOM 当成纯函数）的约束与工程师的实用主义（不强迫工程师只用函数式）。

## 1.1 简介
- React 把真实 DOM 树转换成 JavaScript 对象树，也就是 Virtual DOM
- Virtual DOM 提升了 React 的性能，但这并不是 React 的唯一亮点
- 最大的好处其实还在于方便和其他平台集成
- 函数式编程（对应与声明式编程）才是 React 的精髓

## 1.2 JSX
- 中小写首字母对应 DOM 元素，而组件元素自然对应大写首字母
- JSX 通过命名空间的方式使用组件元素，以解决组件相同名称冲突的问题，或是对一组组件进行归类（相当于大对象）
- 在一个组件的子元素位置使用注释要用 {} 包起来
- class 属性改为 className；for 属性改为 htmlFor
- 在写自定义属性的时候，都由标准写法改为小驼峰写法
- 省略 Boolean 属性值会导致 JSX 认为 bool 值设为了 true，要传 false 时，必须使用属性表达式
- 要使用 HTML 自定义属性，要使用 data- 前缀
- render 方法。它是 React组件生命周期的一部分，也是最核心的函数之一
- 属性值要使用表达式，只要用 {} 替换 "" 即可

## 1.3 React 组件
- Web Components 通过自定义元素的方式实现组件化，而 React 的本质就是关心元素的构成，React 组件即为组件元素
- 组件元素被描述成纯粹的 JSON 对象，意味着可以使用方法或是类来构建
- React 组件基本上由组件的构建方式、组件内的属性状态与生命周期方法组成

React 组件的构建方法
- React.createClass
- ES6 classes
- 无状态函数（stateless function

## 1.4 React 数据流
定义默认 props 配置
```js
static defaultProps = {
	name: 'lili',
	age: 18
};
```

[propsTypes 类型检查](https://blog.csdn.net/suwu150/article/details/79460222)
```js
static propsTypes = {
	String: React.PropTypes.string,
	Number: React.PropTypes.number,
	Function: React.PropTypes.func,
	children: React.PropTypes.oneOfType([
				React.PropTypes.arrayOf(React.PropTypes.node),
				React.PropTypes.node,
	]),
}
```
注意：函数类型的检查是 propTypes.func，布尔类型的检查是 propTypes.bool。

## 1.5 React 生命周期
React 组件的生命周期可以分为挂载、渲染和卸载。可以分两类：
- 当组件在挂载或卸载时
- 当组件接受新的数据时，即组件更新时

**组件的挂载**

```js
import React, { Component, PropTypes } from 'react';

class App extends Component {
	static propTypes = {
	// ...
	};
	
	static defaultProps = {
	// ...
	};
	
	constructor(props) {
		super(props);
		this.state = {
		// ...
		};
	}
	
	componentWillMount() {
	// ...
	}
	
	componentDidMount() {
	// ...
	}
	
	render() {
		return <div>This is a demo.</div>;
	}
}
```
以上代码中，propTypes 和 defaultProps 分别代表 props 类型检查和默认类型。这两个属性被声明成静态属性，意味着从类外面也可以访问它们。

其中 componentWillMount 方法会在 render 方法之前执行，而 componentDidMount 方法会在 render 方法之后执行。

读取初始 state 和 props 以及两个组件生命周期方法 componentWillMount 和 componentDidMount，这些都只会在组件初始化时运行一次。

在 componentWillMount 中执行 setState 方法毫无意义。初始化时的 state 都可以放在 this.state。

**组件的卸载**

组件卸载非常简单，只有 componentWillUnmount 这一个卸载前状态。

```js
import React, { Component, PropTypes } from 'react';

class App extends Component {
	componentWillUnmount() {
	// ...
	}
	render() {
		return <div>This is a demo.</div>;
	}
}
```
在 componentWillUnmount 方法中，我们常常会执行一些清理方法，如事件回收或是清除定时器。

**数据更新过程**

更新过程指的是父组件向下传递 props 或组件自身执行 setState 方法时发生的一系列更新动作

```js
import React, { Component, PropTypes } from 'react';

class App extends Component {
	componentWillReceiveProps(nextProps) {
	// this.setState({})
	}
	
	shouldComponentUpdate(nextProps, nextState) {
	// return true;
	}
	
	componentWillUpdate(nextProps, nextState) {
	// ...
	}
	
	componentDidUpdate(prevProps, prevState) {
	// ...
	}
	
	render() {
		return <div>This is a demo.</div>;
	}
}
```
组件自身的 state 更新了，那么会依次执行 shouldComponentUpdate、componentWillUpdate 、render 和 componentDidUpdate。

shouldComponentUpdate 是一个特别的方法，它接收需要更新的 props 和 state，让开发者增加必要的条件判断，让其在需要时更新，不需要时不更新。因此，当方法返回 false 的时候，组件不再向下执行生命周期方法。

默认情况下，React 会渲染所有的节点，因为 shouldComponentUpdate 默认返回 true。

无状态组件是没有生命周期方法的，这也意味着它没有 shouldComponentUpdate。可以选择引用 Recompose 库的 pure 方法.

不能在 componentWillUpdate 中执行 setState。

componentWillReceiveProps 方法可以作为 React 在 props 传入后，渲染之前 setState 的机会。在此方法中调用 setState 是不会二次渲染的。

## 1.6 React 和 DOM

在 React 组件的开发实现中，我们并不会用到 ReactDOM，只有在顶层组件以及由于 React 模型所限而不得不操作 DOM 的时候，才会使用它。

**ReactDOM 的 API**

- findDOMNode
- render
- unmountComponentAtNode






