#Redux核心

在前面的课程里，你从一个较高层面上浏览了Redux。在这一课程里，我们将学习Redux的基础，包括actions,action creators, reducers和store。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-1-1.mp4{% endvideo %}

Redux难学的一个原因就是，你必须同时弄明白所有的片段是如何拼接在一起的。尽量在下面的课程里弄清楚每一个Redux的概念，这样当把他们拼接起来的时候，你就可以准备好了。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-1-2.mp4{% endvideo %}

![](/assets/store-reducer)
以store为核心，所有的Redux元素都是相互关联的

这个就是我们刚刚看过的图形，在Redux里面，有三个主要的部分:
- Actions
- Reducers
- The store

应用的大多数data或者state存在于store里面。store的data是由reducer填充的(可以有很多的reducer，图片里我们只展示了一个)。Action会被store'dispatch',并且reducers会根据action的种类来决定返回哪些新的数据。为了对应，在Redux应用里当然也不只有一个action。

![](/assets/redux-reducer2)
Redux应用里的数据流。Store会dispatch一个action给它的reducer。