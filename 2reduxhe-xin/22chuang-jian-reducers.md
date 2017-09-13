{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-3-1.mp4{% endvideo %}
**actions**只是负责描述应用里发生的事件--但是它们并不关心也不负责真正的state到底是如何改变的。 这其实是**reducer**的工作。 reducer接受当前的state和被dispatch的action作为参数，然后根据接受的这个action来描述如何将当前的state转换成全新的state。

那么reducer是通过什么方式来根据接受的action类型以确定修改app的state呢？下面看一个例子。

reducer就是一个函数，这个函数接受当前的state和一个从action creator返回的action 对象:
```
function reducer (state, action) {
  // ...
}
```
在reducer内部，我们创建了一个switch表达式，以吻合action的type属性。然后我们返回了一个全新的、更新过的state
```
function reducer (state, action) {
  switch (action.type) {
    case 'SUBMIT_USER' :
      return Object.assign({}, state, {
        user: action.user
      })
  }
}
```

在上面的这个例子里，每当这个`submitUser`action creator被触发并且传递给reducer，我们的额`switch`表达式就会吻合`SUBMIT_USER`case.接着一个新的state就是被创建并且一个`user`属性就会被添加(或者编辑)到这个新的state的`user`属性里，它的值就是我们一开始传入action creator`submitUser`的值。

有一些reducers应当遵循的原则，其中最关键的就是reducers必须得是一个`纯函数(pure function)`

##A Reducer is Pure
>回忆一下纯函数:
1. 传入同样的参数会返回相同的结果
2. 只依赖于传入的参数
3. 不产生任何副作用

reducer的重点就是它会接收当前的state和一个action对象作为参数，然后返回新的state，它只做这些事情。如果你在你的reducer里做了比这更多的事情，那么你的代码可能做了一些错误的事情。Reducer不能够：
- 修改自己的参数
- 产生副作用(包括异步请求、更改局部变量等等)
- 调用其他的非纯函数

换句话说，就是一个reducer应该只是一个纯函数！

![](/assets/Screen Shot 2017-09-13 at 11.18.33.png)

看下面这段代码回答下一个问题

```
function reducer(state = {}, action) {
    switch(action.type){
        case "ADD_ITEM":
            return action.item;
        case "EMPTY_CART":
            return {};
        case "UPDATE_ITEMS":
            state.items = action.items;
            return state;
        default:
            return state;
    }
}
```

![](/assets/Screen Shot 2017-09-13 at 11.19.47.png)

##练习3/3
创建一个自己的reducer。要求:
1. 创建一个被称为"appReducer"的reducer，它接收两个参数:
    - 第一个参数，是一个包含ice cream信息的数组
    - 第二个参数，是一个用`type`属性值为`‘DELETE_FLAVOR’`的对象
2. reducer接收的action对象应该像这样: {type: ‘DELETE_FLAVOR’, flavor: 'Vanilla'}
3. 初始的state应该像这样`[{ flavor: 'Chocolate', count: 36 }, { flavor: 'Vanilla', count: 210 }]`

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-3-2.mp4{% endvideo %}

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-3-3.mp4{% endvideo %}

##Reducers 和 State
Redux里的reducer具体描述了应用的state的信息，并且依据接收的具体的actions来决定如何改变state。

你可以使用ES6的默认特性来初始化reducer的state。
```
function myReducer (state = initialState, action) {
  // ...
}
```
从这个reducer返回的state将成为应用内的新的state，所以你需要确保总是返回新的state或者是之前的state。

```
function myReducer (state = initialState, action) {
  if ( /* ... */ ) {
    return {
      ...state,
      name: 'Tyler'
    };
  }

  return state;
}

```
通过dispatch的action的type，来决定如何更改state。

```
function myReducer (state = initialState, action) {
  if (action.type === CHANGE_NAME) {
    return {
      ...state,
      name: 'Tyler'
    };
  }

  return state;
}
```

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-3-4.mp4{% endvideo %}
[这里是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/9303a724d8fe4388b7c9c2bdbeec8dd9339ad9c1)

确保以下步骤你都做了

![](/assets/Screen Shot 2017-09-13 at 11.47.20.png)

>!Data Normalization!
>当在不同的地方都需要数据的时候如何格式化你的数据呢？首先，你要确保你的数据是标准化的(normalized).后面的教程里会详细讲解

##UI State
能够构建完善的React/Redux应用程序的一个基本部分是了解何时将state存储在Redux中，何时将state存储在React组件中。现在，对于这个没有一套硬套规则，即使是React社区也不能达成一致，所以下面所说的一切都是建议。

在决定一个state到底应该存放在哪里的第一个问题是，“两个组件是否依赖于同一个state？”如果答案是肯定的，那么几乎总是想让Redux管理这个状态。原因是如果将state放在在Redux，无论两个组成部分之间的关​​系如何，每个组织都可以获得所需的state。

我问自己的下一个问题是，“这个状态的缓存story是什么样的？”如果获取数据的操作是很麻烦的，那么可能值得把它放在Redux中，每次组件挂载时都会抓取它。对于任何其他情况，你可能会遵循惯用的本地组件状态。

**Reducers**只是函数，他们接收当前的state和一个action对象作为参数，他们必须是纯函数，并且必须返回一个新的state或者是之前的state

```
function myReducer (state = initialState, action) {
  if (action.type === CHANGE_NAME) {
    return {
      ...state,
      name: 'Tyler'
    };
  }

  return state;
}

```
如果两个组件都依赖于同一个state那么就把state存放在store里，否则获取state的操作会非常expensive








