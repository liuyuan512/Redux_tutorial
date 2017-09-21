{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-5ReduxMiddleware-2-1.mp4{% endvideo %}

![](/assets/redux-middleware)


##Middleware和Redux
你已经知道了单一方向数据流是如何支持Redux应用的可预测性的:要改变store的state，描述变化的action必须得dispatch给reducer。Reducer会返回一个新的state。

在dispatch一个action和rudeucer之间，我们介绍一个可以在它到达reducer之前介入这个过程的被称为**middleware**,即中间件的东西。正如Redux 文档描述的那样，middleware是一个在dispatch一个action和它到达rudeucer之前的一个扩展点。

