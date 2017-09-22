{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-4-1.mp4{% endvideo %}

##背景
目前为止，Redux只支持同步数据流。但是使用像**thunk**这样的中间件就可以支持异步数据了。你可以把thunk想象成store的`dispatch()`方法包装，它不是返回一个action对象，我们可以用**thunk action creators**来dispatch函数或者Promises

注意如果没有thunk，同步触发是默认的。就是说，我们可以在React的组件里使用(比如使用`componentDidMount()`生命周期方法来做请求)，但是有两个问题没有解决:
- 重用性(组件)
- 可预测性,就是只有action creators才可以成为每一个state更新的数据源

下面看一下它是如何工作的

##安装
要使用thunk中间件，确保你安装了[redux-thunk](https://github.com/gaearon/redux-thunk)包
```
npm install --save redux-thunk
```

##Thunk Action Creator Example
假设我们在创建一个能存储用户to-do项目的web应用，当用户登录，app需要从数据库拿到所有用户的to-dos。由于Redux只支持同步数据流，我们可以使用thunk中间件来异步产生这个action的的HTTP请求

在我们写我们自己的thunk action creators之前，先确保我们的stor做好了接收中间件的准备:

```js
// store.js

import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from '../reducers/root_reducer';

const store = () => createStore(rootReducer, applyMiddleware(thunk));

export default store;
```

这样，我们就设置好了应用thunk中间件的每一步:从`redux-thunk`导入了thunk中间件，并且一个thunk实例也被传入了Redux的`applyMiddleware()`enhancer函数

此外，假设我们的HTTP请求是如下这样的:
```js
// util/todos_api_util.js

export const fetchTodos = () => fetch('/api/todos');
```

由于thunk可以让我们写能够返回函数而非对象的action creator，我们新的actioncreator就可以像如下这样:
```js
// actions/todo_actions.js

import * as TodoAPIUtil from '../util/todo_api_util';

export const RECEIVE_TODOS = "RECEIVE_TODOS";

export const receiveTodos = todos => ({
  type: RECEIVE_TODOS,
  todos
});

export const fetchTodos = () => dispatch => (
  TodoAPIUtil
      .fetchTodos()
      .then(todos => dispatch(receiveTodos(todos)))
);

```

`receiveTodos()`是一个返回对象的action creator,有一个`RECEIVE_TODOS`的值

`fetchTodos()`可以使我们返回一个函数，这里我们首先发送HTTP请求到`TodoAPIUtil`.通过创建一个Promise，这个接收所有to-do items的action只有当原始请求c成功时才会被dispatch


##Thunk的底层实现
如果上面的action creator(`fetchTodos()`)不是用thunk中间件写的，那么我们就从reducer得不到理想的回应。毕竟Reducer只接作为纯js对象的actions,而不是作为函数的actions

看一下下面中间件的thunk内部实现的一部分[sorce code]()