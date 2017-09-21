{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-2-1.mp4{% endvideo %}

![](/assets/redux-middleware)


##Middleware和Redux
你已经知道了单一方向数据流是如何支持Redux应用的可预测性的:要改变store的state，描述变化的action必须得dispatch给reducer。Reducer会返回一个新的state。

在dispatch一个action和rudeucer之间，我们介绍一个可以在它到达reducer之前介入这个过程的被称为**middleware**,即中间件的东西。正如Redux 文档描述的那样:
>middleware是一个在dispatch一个action和它到达rudeucer之前的一个扩展点。

一旦中间件收到了这个action，它就会产生一系列的行为，包括:
- 产生一个副作用(比如[logging state](https://github.com/evgenyrodionov/redux-logger))
- 出来它自己的一个行为(比如做一个HTTP请求)
- 将action重新定向(比如转到另一个中间件里)
- 在dispatch过程中运行一些代码
- dispatch一些其他的action

...并且它可以在action传递给reducer之前做任何这些事情

##练习

![](/assets/Screen Shot 2017-09-21 at 15.50.16.png)

##小结
middleware可以在Redux遵循的相同的单向state管理模式下实现。特别的，middleware可以在action到达reducer之前接收action，然后按照指示重新定向action或者产生一个副作用。

下一节会讲述一个产生副作用的一个中间件，叫做**logger**，它会在console里打印有价值的信息

##延伸阅读
- [Middleware from the Redux docs](http://redux.js.org/docs/advanced/Middleware.html)
- [Creating custom Middleware in React/Redux](https://medium.com/@jihdeh/creating-custom-middleware-in-react-redux-961570459ecb)