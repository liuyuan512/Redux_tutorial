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

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-3-2.mp4{% endvideo %}

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-3-3.mp4{% endvideo %}

##Reducers 和 State



