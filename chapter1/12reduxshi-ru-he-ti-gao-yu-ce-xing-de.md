#Redux如何提高预测性
##单向数据流
回忆一下React的一个特性是单向数据流

![](/assets/data-flow.jpg)

在这个图片里，data是存储在父组件里的。如果一个子组件也需要使用这个data，那么这个data就必须传递给这个子组件。任何一个更新都得发送回父组件，在父组件里实施更新，然后更新好的数据再返回给子组件。

React的这个单向数据流工作的挺好，但是当有很多嵌套的子组件时就会出现很多问题

![](/assets/react嵌套)

如果是这种嵌套多层的组件，data就必须被传递到给经过的每一个组件！
{% video %}https://s3.cn-north-1.amazonaws.com.cn/u-vid-hd/aTosJz-N0l4.mp4{% endvideo %}

![](/assets/Screen Shot 2017-09-07 at 11.25.21.png)

##小结
Redux在一些方面提升了web应用的预测性:
- Data被放在一个地方几种管理
- 组件必须请求访问该数据
- store里面的额data是单一方向流
- store 更新的规则很严格