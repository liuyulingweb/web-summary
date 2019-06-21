1.6.4 React 之外的 DOM 操作
  ReactDOM.findDOMNode
 
1.7 组件化实例：Tabs 组件
  import classnames from 'classnames';
 
2.1.2 合成事件的实现机制
  在 React 底层，主要对合成事件做了两件事：事件委派和自动绑定
  1. 事件委派
   并不是将事件绑定在真实的节点上。而是把所有事件绑定在结构的最外层，使用一个统一的事件监听器，这个事件监听器维持了一个映射来保存所有
   组件内部的事件监听和处理函数，当组件挂载或卸载时，只是在这个事件监听器上插入或删除一些对象。当事件发生时首先统一处理。在映射里找到
   真正的事件处理函数并调用。
  2. 自动绑定
  bind 方法：<button onClick={this.handleClick.bind(this, 'test')}>Test</button>
  构造器内声明： this.handleClick = this.handleClick.bind(this)
  箭头函数
  
2.1.3 在React 中使用原生事件
   componentDidMount 会在组件已经完成安装并且在浏览器中存在真实的 DOM 后调用，此时我们就可以完成原生事件的绑定。
   在 React 中使用 DOM 原生事件时，一定要在组件卸载时手动移除，否则很可能出现内存泄漏的问题。而使用合成事件系统时则不需要，因为 React
   内部已经帮你妥善地处理了。
   ```
   componentDidMount() {
    this.refs.button.addEventListener('click', e => {
    this.handleClick(e);
   });
    }
   handleClick(e) {
    console.log(e);
   }
   componentWillUnmount() {
    this.refs.button.removeEventListener('click');
   }
```
 
2.1.4 合成事件与原生事件混用
  React 合成事件系统的委托机制，在合成事件内部仅仅对最外层的容器进行了绑定，并且依赖事件的冒泡机制完成了委派。也就是说，事件并没有直接
  绑定到元素上，所以在这里使用 e.stopPropagation() 并没有用。
  解决方法：不要将合成事件与原生事件混用或者通过 e.target 判断来避免(e.target && e.target.matches('div.code')
  
  尽量避免在 React 中混用合成事件和原生 DOM 事件。
  另外，用 reactEvent.nativeEvent.stopPropagation() 来阻止冒泡是不行的。阻止 React 事件冒泡的行为只能用于 React 合成事件系统中，且
  没办法阻止原生事件的冒泡。反之，在原生事件中的阻止冒泡行为，却可以阻止 React 合成事件的传播。
  
  React 的合成事件系统只是原生 DOM 事件系统的一个子集。它仅仅实现了 DOMLevel 3 的事件接口，并且统一了浏览器间的兼容问题。有些事件 React
  并没有实现，或者受某些限制没办法去实现，比如 window 的 resize 事件。
  
 2.1.5 对比React 合成事件与JavaScript 原生事件
  1. 事件传播与阻止事件传播
  阻止原生事件传播需要使用 e.preventDefault()，不过对于不支持该方法的浏览器（IE9 以下），只能使用 e.cancelBubble = true 来阻止。而在
  React 合成事件中，只需要使用 e.preventDefault() 即可。
  2. 事件类型
  React 合成事件的事件类型是 JavaScript 原生事件类型的一个子集。
  3. 事件绑定方式
  原生： 直接在 DOM 元素中绑定；在 JavaScript 中，通过为元素的事件属性赋值的方式实现绑定；通过事件监听函数来实现绑定
        el.addEventListener('click', () => {}, false);
        el.attachEvent('onclick', () => {});
  React: <button onClick={this.handleClick}>Test</button>
  4. 事件对象
  原生 DOM 事件对象在 W3C 标准和 IE 标准下存在着差异
  
2.4 组件间通信
  2.4.1 父组件通过 props 向子组件传递需要的信息
  2.4.2 子组件向父组件通信
    利用回调函数 利用props回调
    利用自定义事件机制
  2.4.3 使用 context 来实现跨级父子组件间的通信  getChildContext() -> this.context
  2.4.4 没有嵌套关系的组件通信,自定义事件机制
    在 componentDidMount 事件中，如果组件挂载完成，再订阅事件；当组件卸载的时候，在 componentWillUnmount 事件中取消事件的订阅。
    emitter.emit('ItemChange', entry) -> emitter.on('ItemChange', (data)）
    
2.5 组件间抽象
  2.5.1 mixin
  
2.6.1 纯函数
纯函数由三大原则构成：
  给定相同的输入，它总是返回相同的输出；
  过程没有副作用（side effect）；
  没有额外的状态依赖
KISS原则（Keep It Simple,Stupid）：在简洁性与傻瓜化；

为了避免浅拷贝带来的负面影响，提出了 Immutable 原则，可以借用 lodash 的 cloneDeep 来解决。

2.6.2 PureRender
可以使用官方的插件，其名为 react-addons-pure-render-mixin。  
this.shouldComponentUpdate = PureRenderMixin.shouldComponentUpdate.bind(this);  
return <div className={this.props.className}>foo</div>;

利用 Immutable.is 优化后的 shouldComponentUpdate:
```
import React, { Component } from 'react';
import { is } from 'immutable';
class App extends Component {
	shouldComponentUpdate(nextProps, nextState) {
		const thisProps = this.props || {};
		const thisState = this.state || {};
		if (
			Object.keys(thisProps).length !== Object.keys(nextProps).length ||
			Object.keys(thisState).length !== Object.keys(nextState).length
		) {
			return true;
		}
		for (const key in nextProps) {
			if (nextProps.hasOwnProperty(key) && !is(thisProps[key], nextProps[key])) {
				return true;
			}
		}
		for (const key in nextState) {
			if (nextState.hasOwnProperty(key) && !is(thisState[key], nextState[key])) {
				return true;
			}
		}
		return false;
	}
}

```

2.6.4 key
有两个子组件需要渲染的时候，我们没法给它们设 key。这时需要用到 React 插件 createFragment 来解决
  
2.6.5 react-addons-perf（性能检测）
React 提供的 TransitionGroup 能够帮助我们便捷地识别出增加或删除的组件，从而让我们能够专注于更加简单的属性变化的动画。

2.7.1 CSS 动画与 JavaScript 动画
1. CSS 动画的局限性
	- CSS 只支持 cubic-bezier 的缓动，如果你的动画对缓动函数有要求，就必须使用 JavaScript动画。
	- CSS 动画只能针对一些特有的 CSS 属性。仍然有一些属性是 CSS 动画不支持的，例如SVG 中 path 的 d 属性。
	- CSS 把 translate、rotate、skew 等都归结为一个属性——transform。因此，这些属性只能共用同一个缓动函数。例如，我们想要动画的轨迹是一条贝塞尔曲线，可以通过给 left和 top 这两个属性加两个不同的 cubic-bezier 缓动来实现，但是 left 和 top 实现的动画性能不如 translateX 和 translateY。
	
2. CSS animation


3. 用 JavaScript 包装过的 CSS 动画
使用 react-smooth 库来写动画。

4. JavaScript 动画
JavaScript 动画包含缓动函数部分和渲染部分。

5. SVG 线条动画
说起 SVG 线条动画，最出名的恐怕是 vivus.js，它巧妙地利用了 SVG path 的 stroke-dasharray属性和 getTotalLength 方法。

spring 动画->react-motion 库


2.8 自动化测试
