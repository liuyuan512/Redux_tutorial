{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-5-1.mp4{% endvideo %}

[这是一些React代码](https://github.com/udacity/reactnd-udacimeals-complete/blob/d0d4b8ade3dea46b7a3250ea196e0f862a399672/src/components/App.js)，下面视频我们会写入，你可以知己copy过来。我们将在我们的App组件里渲染它。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-5-2.mp4{% endvideo %}
[这里是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/d0d4b8ade3dea46b7a3250ea196e0f862a399672)

![](/assets/Screen Shot 2017-09-13 at 14.37.04.png)


>!The `ref` 属性!
>上一个视频里使用了`ref`这个属性。`ref`属性时React提供的一个特殊属性，它使你可以访问DOM。更多关于`ref`的信息以及如何使用，点击[Refs and the DOM documentation](https://facebook.github.io/react/docs/refs-and-the-dom.html)

![](/assets/Screen Shot 2017-09-13 at 14.42.23.png)

##小结
**Actions**会被diapatched进入**store**的**reducer**里，告诉它应该更新的信息。由于这三个核心概念会相互交融来帮助管理应用的state，分开学习他们会有点奇怪。所以刚刚接触会有点晕，可以多看几遍。