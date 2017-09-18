![](/assets/Screen Shot 2017-09-18 at 18.10.37.png){% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-4ArchitectReduxStore-2-1.mp4{% endvideo %}

##Reducer Composition
到目前为止，我们只有一个reducer。只有一个reducer可以工作，但是随着应用变得越来越大，它会很难管理。 假设我们有一个"users"的reducer:
```js
function users (state = {}, action) {
  switch (action.type) {
    case 'ADD_USER' :
      return {};
    case 'REMOVE_USER':
      return {};
    default :
      return state;
  }
}
```
如果我们想要向我们的Redux store添加一个books呢？ Users和books是两种完全不同的数据。让users这个reducer来管理books的state有点不太合理。这就需要再创建一个新的reducer:
```js
function users (state = {}, action) { 
  // ... 
}

function books (state = {}, action) { 
  // ... 
}
```
我们已经将我们的reducer分开来处理不同的state。这个过程叫做**reducer composition**。然而我们就会出现一个新的问题:Redux的`createScore()`方法只接收一个reducer。为了创建一个稳定的store,我们需要找出一种可以把这几个reducer组合成一个reducer的方法。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-4ArchitectReduxStore-2-2.mp4{% endvideo %}
[这里是视频中更改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/f92571e94b6b42cad3391983887261d91192a775)

##combineReducers()
直到目前为止，这个state树的形状还是很简单，也许如下面这样:
```js
const initialState = {
  data: [],
  isFetching: false,
  error: ''
}

```
但是你可以想象一下，随着我们的应用变得越来越复杂，我们会想要创建不止一个reducer，这样就可以管理不同的state了。我们想要将上面那种store改造成这样:
```
{
  users: {},
  modal: {},
  posts: {},
  replies: {},
  listeners: {}
}
```
我们可以通过**reducer composition**，来使得每一个reducer管理每个分离、独立的state部分。通过这种方式，每一个reducer就可以只接收state里特定的那部分，比如replies reducer只接收state里"replies"的那部分state。类似的，users reducer只接收state里"users"那部分state。当我们增长为更多的reducer时，同样的模式同样适用:一个reducer只接收一个state和一个action，并且返回一个新的，修改过的这个部分的state。我们实现这个的方式就是首先先创建多个reducer，然后用Redux's `combineReducers()`方法。

`combineReducers()`是Redux提供的一个辅助方法，它可以将值为不同的reducer 函数的对象转变成一个唯一的reducer 函数。然后我们将这个"root reducer"传递给`createStore()`来创建这个应用的store.下面看一下它是如何工作的:

```js
// reducers/root_reducer.js

import { combineReducers } from 'redux';

function users (state = {}, action) {
  // ...
}

function books (state = {}, action) {
  // ...
}

export default combineReducers({
  users,
  books,
});

```

```js
// store/store.js

import rootReducer from '../reducers/root_reducer';

const store = createStore(rootReducer)
console.log(store.getState()) // { users: {}, books: {} }
```

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-4ArchitectReduxStore-2-3.mp4{% endvideo %}
[这里是视频中修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/8948986f81b9ff82640a484037445ecbbfc5dc8f)

##确保你跟上了节奏
![](/assets/Screen Shot 2017-09-18 at 18.08.23.png)


##练习
![](/assets/Screen Shot 2017-09-18 at 18.09.52.png)

![](/assets/Screen Shot 2017-09-18 at 18.10.37.png)


