{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-2-1.mp4{% endvideo %}
浏览器允许你设立事件监听器和对某些事件进行响应。Redux同样，只是这些事件被称为**actions**。这些你创建的actions是信息的载体，用来描述应用里应该更新state的任何的事件。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-2-2.mp4{% endvideo %}
Actions只是一个JavaScript对象，用来描述应当更新的state的任何事件。这些对象里应当包含一个`type`属性，为了区别每一种事件类型。
```
const LOAD_PROFILE = 'LOAD_PROFILE';

const myAction = {
  type: LOAD_PROFILE
};
```
表示所发生的操作类型所需要的任何其它数据都可以作为action中的属性传递。

>##!Action 建议!
>一些你在创建Action 对象时需要注意的
>- action的`type`属性尽量用常量表示，而不要用字符串。当然常亮和字符串都可以工作，但是当使用常量的时候，如果发生拼写错误就会在console里抛出一个错误，但是字符串就会没有任何反应。
- 尽可能使你的信息载体小一点。使你的资源仅传递必要的data。