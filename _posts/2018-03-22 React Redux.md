---
layout: post
title: React Redux
date: 2018-03-22 07:24:00
---

# 什么是 Redux？
Redux 可以说是 Flux 架构思想的最佳实践方案，用于对大型、复杂、多数据来源的 React 进行数据管理

# Redux 设计的三大原则
1. 单一的数据来源，所有的数据保存在一个对象中
2. 状态只读，Reducer 根据自 store dispatch 的 action 类型返回一个新的状态，不修改原来的状态
3. 状态修改均由纯函数完成

# Redux 核心 API
1. store
store 作为整个应用数据的唯一来源，用于保存数据和 dispatch action。store 使用 Redux 提供的 createStore 方法用于生成
```
import { createStore } from 'redux';
let store = createStore(reducer)
```
createStore 接受一个 reducer 作为参数，返回一个 store 对象。store 对象包含 4 中方法:
getState()：用于获取 store 中当前的状态
dispatch()：用于分发 action，这个是改变 store 中数据的唯一方式
subscribe(listener)： 注册一个监听者，在 store 发生变化时被调用
replaceReducer(nextReducer)：更新当前 store 中的 reducer

2. reducer
reducer 本质上是一个函数，这个函数能接受一个 action 和一个旧的状态（previousState）,根据 previousState 和 action 返回新的状态
```
reducer(previousState, action) => newState
```

3. action
reducer 的 action 本质上是一个 javaScript 对象，这个对象必须有一个 type 属性，用来表明 action 的类型，还可以有 payload, error, meta 属性。关于 action 对象的属性，社区有个规范，可以[参考](https://github.com/redux-utilities/flux-standard-action)
```
const action = {
  type: 'ADD_TODO',
  payload: 'todo'
}
```
reducer 就是根据 action type 属性来决定返回新的 state。

通过上面简单的学习，我们大概明白了 Redux 这样的一个工作流程：
view 层触发一个 action，这个 action 由 store.dispatch(action) 传递给 reducer，reducer 根据 previousState 和 action type 返回一个新的 state（不修改数据）, 如此实现了数据的变更。

现在我们来看一个最小的 redux 应用。实现点击按钮让数字加一减一这么个简单应用。

demo 地址: []()

我在学习 Redux 的时候，看了很多文档，认为对 Redux 的概念了然于胸，但是动手写第一个小 demo 的时候仍然觉得很难下手，可能是 Redux 这些概念对我而言太新。这里给出我写的第一个小 demo，为了能更加直观的了解 ```action```、```store```、```reducer``` 之间的关系，我将这个小 demo 核心代码写在了一个文件中

```
import React from 'react';
import ReactDOM from 'react-dom';

// 创建 action
// action 是 javaScript 对象，使用户行为的抽象，必须包含一个 stype 字段
// 根据 demo 需要实现的记数功能，抽象出两种 action,一种表示加，一种表示减
const incream_action = { type: 'INCREAM' };
const decream_action = { type: 'DECREME' };

// 创建 reducer
// reducer 接受一个 previousState 和 action 返回一个新的 state
const reducer = (state=0, action) => {
  switch (action.type) {
    case incream_action.type:
      return state + 1;
    case decream_action.type:
      return state - 1;
    default:
      console.log('default');
      return state;
  }
}

// 创建 store
// store 创建使用 createStore(reducers)
// createStore 由 redux 提供
import { createStore } from 'redux';
let store = createStore(reducer);


class Counter extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    const { count, onIncrement, onDecrement } = this.props
    return(
      <div>
        <span>{count}</span>
        <button onClick={onIncrement}>+</button>
        <button onClick={onDecrement}>-</button>
      </div>
    )
  }
}

const render = () => ReactDOM.render(
  <Counter
    count={store.getState()}
    onIncrement={() => store.dispatch(incream_action)}
    onDecrement={() => store.dispatch(decream_action)}
  />,
  document.getElementById('root')
);

render();

// 为了能在 store 发生变化后能刷新页面，需要给 store 注册一个监听事件
// store 变化后，刷新页面
store.subscribe(render);

```
