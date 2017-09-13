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

