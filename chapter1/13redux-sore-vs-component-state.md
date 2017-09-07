{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-1WhyRedux-4-1.mp4{% endvideo %}

Redux是一个web应用里面强大state容器，但是并没有强制的规则要求所有的state都必须存储在Redux store里面。实际上把一些data存放在React组件内部也是很合理的。最终存放在哪里是有你做决定的，但是你也可以遵循一些常见的惯例。

##Redux Store
一般来说，如果state需要再应用内部全局共享和访问，那么state就需要存放在store里面。例子包括:
- 缓存的用户
- email的草稿

##Component state
如果是一些很多"本地化"的数据，或者说你需要处理的state并不会影响其它的组件，那么组件的state就是一个不错的选择。例子包括:
- Form input
- 