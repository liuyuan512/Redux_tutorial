{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-3React&Redux-2-1.mp4{% endvideo %}

##安装
在我们使用**Provider**之前，我们需要先安装它：
```
npm install --save react-redux
```

同样确保从`'react-redux'`里导入Provider
```
import { Provider } from 'react-redux';
```

##使用Provider组件

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-3React&Redux-2-2.mp4{% endvideo %}
[这里是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/b8d39c14c22f7b9067a807a3a76ae133923b1669)

![](/assets/Screen Shot 2017-09-13 at 16.23.03.png)

##使用Provider
Provider的厉害之处在于它的context特性，React文档是这么描述的:
>"In some cases, you want to pass data through the component tree without having to pass the props down manually at every level. You can do this directly in React with the powerful 'context' API"

Provider使connect()实现的原因是，正如文档里描述的那样，Provider让”向组件传递数据，不用手动的向组件树的每一层传递props了“

![](/assets/Screen Shot 2017-09-13 at 16.29.59.png)

##Provider小结
Provider使Redux向需要store的state的React组件传递state变得易于操作。它用到了React的[context](https://facebook.github.io/react/docs/context.html)特性来使它得以实现。

然而，组件需要访问到store,还需要一个方式来"connect"它们。我们之前提到过`connect()`函数，它用到了一个函数编程里被称为**currying**的技术。在我们实际看`connect()`之前，我们先来看一下currying的原理。