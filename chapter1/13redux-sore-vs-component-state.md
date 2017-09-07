{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-1WhyRedux-4-1.mp4{% endvideo %}

Redux是一个web应用里面强大state容器，但是并没有强制的规则要求所有的state都必须存储在Redux store里面。实际上把一些data存放在React组件内部也是很合理的。最终存放在哪里是有你做决定的，但是你也可以遵循一些常见的惯例。

##Redux Store
一般来说，如果state需要再应用内部全局共享和访问，那么state就需要存放在store里面。例子包括:
- 缓存的用户
- email的草稿

##Component state
如果是一些很多"本地化"的数据，或者说你需要处理的state并不会影响其它的组件，那么组件的state就是一个不错的选择。例子包括:
- Form input
- 当前选中的tab
- 下拉开关状态

无论你选择什么，要确保它对你的应用是合适的。正如Dan Abramov在Redux文档里建议的那样:
>There is no "right" answer for this... As a developer, it is your job to determine what kinds of state make up your application, and where each piece of state should live. Find >a balance that works for you, and go with it.

##Redux State是只读的
Redux store里面的state是只读文件。实际上这个只读属性也是[Redux三大基本原则](https://github.com/reactjs/redux/blob/master/docs/introduction/ThreePrinciples.md#state-is-read-only)之一
- 可预测性和稳定性得到了提升
- 避免了副作用
- 减少了写入state的外部资源
- 所有的更新被集中到了一个地方并且是一个一个有次序的发生

改变state的唯一方式，就是触发一个**action**,它是用来面试你要做出的改变。

##小结

尽管Redux提供了一个唯一数据源，但是在组件的内部状态中存储一些数据是完全没有问题的。
在Store里的全局的state情况下,Redux会对于更新state提出严格的规则限制。其中之一就是在Redux应用里，只有纯函数才能更新state。

##延伸阅读
- [State is Read-Only](https://github.com/reactjs/redux/blob/master/docs/introduction/ThreePrinciples.md#state-is-read-only) 
- [How to choose between Redux's store and React's state?](https://github.com/reactjs/redux/issues/1287)
- [Organizing State](http://redux.js.org/docs/faq/OrganizingState.html)