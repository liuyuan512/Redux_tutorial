#为什么要使用Redux?

{% video %}https://s3.cn-north-1.amazonaws.com.cn/u-vid-hd/CFI1O4NI4NU.mp4{% endvideo %}

#Redux聚焦于State管理
官方的Redux文档是这样描述Redux的
>a predictable state container for JavaScript apps.

你或许会好奇，如果React已经可以管理前端应用的state，那么为什么Redux还会存在呢?

使用Redux的最主要的好处体现在你的应用内需要共享state的时候。当有两个组件都需要访问同一个state的时候，这个state就称为"shared state"。当你在父子组件内传递state时，你可以将父组件的state作为子组件的props传递进来。但是如果是一个组件有多级后代，比如它是一个组件的爷爷的爷爷的爷爷的组件，那么你就必须得一级一级的传递props。而且在这个过程中，经手的组件根本不需要访问这个state。

当创建一个web应用时，Redux不仅会提供一个存储data的规范的方式，它还可以让我们在应用内的任何地方快速获取这个data。你只需要告诉Redux哪个组件需要哪个data，redux自己会处理剩下的事情。

有了Redux，你就可以随心所欲的控制state。

#The Store:唯一数据源
Redux最基本的原则之一是Redux只有唯一的一个单一数据源:the store。也就是说，store包含了应用的全局state，所有的state都被存放在一个对象树里。

只有一个state树会使应用在很多方面受益。假设你要在一个应用内实现一个Undo/Redo特性，如果所有的state都被存储在一个树里(单一数据源)，那么这样实现起来会比data通过很多组件传递实现简单的多。将state放在一个集中的地方管理，调试和检查会变得更加简单和直观。

为了维持这个唯一数据源，Redux实现了一些规则来使事情更加直观。首先，Redux里面的state是只读属性的，也就是说，Redux的state是不可更改的。例如，React组件不能直接写进Redux State里面。必须得通过表达一个意愿来更新state。

只有被称为`reducers`的纯函数有修改state的能力。先不要担心这些名词，下一节会深入讲解。

![](/assets/Screen Shot 2017-09-06 at 16.44.15.png)

随着单页应用变得越来越复杂，恰当的state管理会变得空前重要。例如，为了管理比如表单state这样的data，一个应用或许需要管理：
- 服务端响应
- 缓存数据(比如用户)
- 还未同步到服务端的本地数据

在此之上，UI的state也会变得更加复杂。同样的这个应用或许还需要追踪:
- 激活路由
- 当前选中的标签
- 分页控件

Redux的诞生就是为了解决上述问题的。它的创建者，Dan Abramov，采用了[Elm programming language](https://github.com/evancz/elm-architecture-tutorial/)的一些技巧，2015年在[Flux](https://facebook.github.io/flux/docs/overview.html)的基础之上，创建了Redux。从那时起，Redux经历的飞速的发展，每月都有几百万的下载量。

#小结
Redux是一个用来管理应用前端state的JavaScript库。Redux并不是React应用所必须的，但是随着web应用变得越来越复杂，因为管理state错误而引发的bug就会越来越多。Redux应用的全局state会在唯一数据源：the store里面被管理。由于state的更新被严格控制着，这使得Redux应用变得非常的可预测。事实上，最主要的[开发者喜欢Redux的原因](https://stackshare.io/reduxjs)就是Redux的可预测性。 下面我们来一起探寻原因。

#延伸阅读
- [Motivation](http://redux.js.org/docs/introduction/Motivation.html)from the Redux docs
- [Three Principles of Redux](http://redux.js.org/docs/introduction/ThreePrinciples.html#three-principles)
- [Redux on GitHub](https://github.com/reactjs/redux)
- [Redux on npm](https://www.npmjs.com/package/redux)