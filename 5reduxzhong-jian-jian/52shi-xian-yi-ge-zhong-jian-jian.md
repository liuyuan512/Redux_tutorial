{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-3-1.mp4{% endvideo %}

##Middleware应该放在Redux应用哪里呢？
我们是用`createStore()`方法用来创建Redux store。除了向这个函数传递一个reducer参数以外，`createStore()`同样还接受一个可选参数`enhancer`,下面是`createStore()`方法的特性:
```js
store.createStore(reducer, [preloadedState], [enhancer])
```

Redux给我们提供了`applyMiddleware()`函数，它可以用作`enhancer`的参数。`applyMiddleware()`可以接受收很多参数，如果需要，我们可以在一个应用里用多个中间件。下面看一下**logger**中间件是怎么实现的！

##例子:logger中间件
Redux是一个web端可预测的state容器。当一个action被diapatch，会返回一个新的state(state不能自己更新，也不能被任何一个外部资源写入)。那么，将应用里发生的每一个action和state都在之前和之后打印岂不是更好？

我们可以用**logger**中间件来做这件事情。这个logger产生了一个副作用:在reducer执行action之前和之后都打印store的state

下面看一下具体怎么实现

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-3-2.mp4{% endvideo %}

