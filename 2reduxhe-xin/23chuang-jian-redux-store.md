{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-4-1.mp4{% endvideo %}

要创建store，你需要将reducer函数作为第一个参数传递给`createStore`。从`createStore`返回的值就是store，store有三个属性:
- `getState()`
- `dispatch()`
- `subscribe()`

##getState()
`store.getState()`没有任何参数，它返回store里的当前state。

##dispatch()
`store.dispatch(action)`接收一个action对象作为参数，并且会调用reducer函数，将当前的state和dispatch的action传递给他。例如：
```
// store.js

import { createStore } from 'redux';
import reducer from '../reducers/reducer';

let store = createStore(reducer);

const receiveComment = comment => ({
  type: 'RECEIVE_COMMENT',
  comment
});

export default store;
```

```
store.getState(); // []
store.dispatch(receiveComment('Redux is great!'));
store.getState(); // ['Redux is great!']
```

##subscribe()
`store.subscribe(cb)`接收一个回调函数作为参数，这个函数会当store里面的state发生变化时立刻被调用。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-4-2.mp4{% endvideo %}
[视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/e326c9569d89abc53da12ecd06f62f2c0c7a9389)

![](/assets/Screen Shot 2017-09-13 at 14.09.41.png)

