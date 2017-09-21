{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-3-1.mp4{% endvideo %}

##Middleware应该放在Redux应用哪里呢？
我们是用`createStore()`方法用来创建Redux store。除了向这个函数传递一个reducer参数以外，`createStore()`同样还接受一个可选参数`enhancer`,下面是`createStore()`方法的特性:
```js
store.createStore(reducer, [preloadedState], [enhancer])
```

Redux给我们提供了`applyMiddleware()`函数，它可以作为`enhancer`这个参数。`applyMiddleware()`可以接受收很多参数，如果需要，我们可以在一个应用里用多个中间件。下面看一下**logger**中间件是怎么实现的！

##例子:logger中间件
Redux是一个web端可预测的state容器。当一个action被diapatch，会返回一个新的state(state不能自己更新，也不能被任何一个外部资源写入)。那么，将应用里发生的每一个action和state都在之前和之后打印岂不是更好？

我们可以用**logger**中间件来做这件事情。这个logger产生了一个副作用:在reducer执行action之前和之后都打印store的state

下面看一下具体怎么实现

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-3-2.mp4{% endvideo %}
[这里是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/2b60fe731b2e4f8ebcfaaafc0ac36ecd11e5215d)

>##!The redux-logger npm Package!
>在之前的视频里，我们应用了自定义的logger来打印state.同样可以点击[redux-logger](https://www.npmjs.com/package/redux-logger),安装:
```
npm install --save redux-logger
```
>redux-logger软件包随附了默认选项,你可以添加自定义选项如果需要[further customizations](https://github.com/evgenyrodionov/redux-logger#options)

##练习
![](/assets/Screen Shot 2017-09-21 at 16.50.31.png)

##小结
我们在Redux应用里的一个集中的地方应用了中间件:就是创建一个store的时候。`createStore()`方法接收一个必须的`reducer`作为参数，但是我们还可以传入一个可选参数`enhancer`。这个参数可就是Redux的`applyMiddleware() `函数，它本身可以接收多个中间件实例。

##延伸阅读
- [redux-logger](https://github.com/evgenyrodionov/redux-logger)